# Issue

**Title:** feat(backend): add opt-in LOG_FORMAT and LOG_LEVEL settings

## Description

## What does this change?

Two new settings. `LOG_FORMAT=legacy|json|text` (case-insensitive) picks the format of application logs on stdout: `legacy` (default) is today's mix of JSON from `log_structured` and plain text from stdlib loggers; `json` makes every log line JSON (stdlib, Celery, uvicorn); `text` makes every log line readable. `LOG_LEVEL=DEBUG..CRITICAL` (case-insensitive, `WARN` and `FATAL` accepted as aliases, other values ignored with a warning) applies one threshold to what is printed, `log_structured` included. `.env.example` lists both, commented out with their defaults, like the other optional settings.

## Why?

Local logs are hard to read (JSON from app code, text from the rest), and production logs cannot be parsed by a collector in one pass because only `log_structured` lines are JSON. Unset, nothing changes: `log_structured` keeps its `print`, and the stdlib/Celery/uvicorn handlers are untouched.

I did not route `log_structured` through the logging module. That would change the default output in ways that are hard to see: Sentry's logging integration would turn the ~116 error-level calls into events, `basicConfig` in scripts would reformat them, loggers disabled by Alembic's `fileConfig` would drop them, and an unserializable value would print `--- Logging error ---` instead of raising.

Details worth a look:

- `log_structured` serializes before filtering, so an unserializable attribute raises the same `TypeError` in every format and also when `LOG_LEVEL` filters the call out. Otherwise `text` in development would hide a crash that `legacy` hits in production.
- `LOG_LEVEL` is set on the handlers as well, so loggers with their own level (`httpx`, `httpcore` at WARNING) cannot print below it. It cannot lower those libraries below WARNING. Sentry sees records by logger level, not handler level: with `CRITICAL`, errors logged by app, Celery and uvicorn code no longer become Sentry events, while `httpx`/`httpcore` errors still do. Documented.
- `LOG_LEVEL` is a common variable name. A value the backend does not know (anything but the five level names and `WARN`/`FATAL`, e.g. `TRACE` set for another tool) is ignored with a warning at startup, as if it were unset, so existing deployments keep starting.
- Output printed outside logging keeps its own format: CLI and Celery banners, uvicorn's first lines and reloader messages, start script traces, migrations and seeds, raw payloads with `RAW_PAYLOAD_STORAGE=log`, Python warnings. In `legacy`, uvicorn's lines go to stderr as before. Documented in `docs/deployment/docker.mdx`.
- The default becomes `text` in a later breaking release; the docs say so. The production override table in the Docker guide suggests `LOG_FORMAT=json` when a log collector reads the output.
- `tests/__init__.py` pins `LOG_FORMAT=legacy` before the app is imported, so a developer's `config/.env` cannot change what the tests parse.

## How did you test this?

A script that emits a fixed set of records (stdlib with traceback, `log_structured` at every level, colliding attribute names, `%s`, context trace id, UUID, an unserializable value, Celery and uvicorn loggers), run on `main` and on this branch:

| Settings | stdout/stderr vs main |
|---|---|
| unset | identical |
| `LOG_FORMAT=legacy` | identical |
| `LOG_LEVEL=DEBUG` | identical plus the two debug lines |

`fastapi run` against `main` and this branch with defaults: identical stdout and stderr (re-checked on the final version). On an earlier revision a reviewer also compared `fastapi dev` with a reload, a Celery worker with a task, beat and flower against `main`: identical; the later changes do not touch the default path (`configure_logging()` does nothing with defaults). With `json`:

```
{"timestamp": "...", "level": "info", "message": "Application startup complete.", "logger": "uvicorn.error"}
{"timestamp": "...", "level": "error", "message": "http_request", "provider": null, "method": "GET", "path": "/nonexistent-path", "status": 404, "duration_ms": 0.7}
```

and with `text`:

```
14:03:14.182 ERROR    app.access  http_request  method=GET path=/nonexistent-path status=404 duration_ms=0.7
```

`tests/utils_tests/test_logging_setup.py` pins the legacy output byte for byte (recorded from `main`) and covers the formats, `LOG_LEVEL` on loggers with their own level, `TypeError` in every format, settings validation, the real uvicorn-then-lifespan sequence and the Celery setup. Full backend suite: 2697 passed, 2 skipped.

## AI usage

Claude Code (Claude Opus 5.5) wrote the change and the tests; the change was reviewed with Claude subagents and OpenAI Codex.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Backend logs can use legacy, JSON, or readable text formats.
  * Set a minimum log level to filter output; `WARN` and `FATAL` are supported as aliases.
  * Structured logs include timestamps and relevant context in the selected format.
* **Bug Fixes**
  * Invalid structured log values raise an error even when the entry is filtered out.
* **Documentation**
  * Deployment guides describe logging formats, levels, and configuration defaults.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac9f948ffd22`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.