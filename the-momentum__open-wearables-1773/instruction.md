# Issue

**Title:** chore(backend): upgrade FastAPI to 0.142.2 with its OpenTelemetry support off

## Description

## What does this change?

Bumps FastAPI to 0.142.2 and passes `telemetry={"auto_configure": False, "tracing": False, "metrics": False, "logs": False}` to `FastAPI()`.

## Why?

FastAPI 0.142.0 added built-in OpenTelemetry (fastapi/fastapi#16403), on by default. As soon as any OpenTelemetry provider is installed, it records request traces, metrics and exception logs; with the OTLP exporter packages present and `OTEL_EXPORTER_OTLP_ENDPOINT` set, it also installs exporters itself. The next routine dependency bump would pull that in. This turns it off, and prepares for an opt-in log export that installs its own provider: `auto_configure: False` alone would not be enough there, the three signal flags are what keep FastAPI quiet once a provider exists.

`>=0.142.2`: 0.142.1 builds included-router handlers once instead of per request (and 0.142.0/0.142.1 could fail at startup when automatic configuration failed, which no longer applies with `auto_configure` off). Diffing the 0.141.1 and 0.142.2 wheels shows functional changes only in `telemetry/` (new), `routing.py`, `applications.py`, `background.py`; OpenAPI output is unchanged (`scripts/export_openapi.py --check`) and Sentry 2.70 produces the same events and transaction names on both versions.

From 0.142, `import fastapi` imports `opentelemetry.propagate`, which reads `OTEL_PROPAGATORS`. A propagator that is not installed (`OTEL_PROPAGATORS=b3`) stops anything that imports FastAPI (the app, `export_openapi.py`, the tests) with `ValueError: Propagator b3 not found`. Documented in `docs/deployment/docker.mdx`; please also put it in the release notes.

## How did you test this?

API started with `TestClient` (lifespan + one request), `OTEL_EXPORTER_OTLP_ENDPOINT=http://127.0.0.1:4318`, OpenTelemetry SDK installed by hand (it is not in this branch's lock):

| | global providers | FastAPI warnings | exports |
|---|---|---|---|
| 0.142.2, no `telemetry=` | SDK Tracer/Meter/LoggerProvider | none | trace and metric export attempts to :4318 |
| this branch | proxies (no-op) | none | none |

`tests/utils_tests/test_fastapi_telemetry.py` runs the app in a fresh process, once without providers and once with recording providers installed before the app is imported, and requests `/openapi.json`, a validation error (400 in this app) and an unhandled exception. It asserts that no provider is used and FastAPI logs nothing, with a positive control: a plain `FastAPI()` in the same process does use the providers. It fails for each of these mutants: no `telemetry=`, only `auto_configure: False`, and each of `tracing`/`metrics`/`logs` switched back on. `auto_configure` itself cannot be observed while all three signals are off; it is set for the day one of them is turned on. The child process has Sentry and outgoing webhooks off, since it does not get conftest's mocks.

`uv.lock`: only `fastapi` and the new `opentelemetry-api` change. Full backend suite: 2652 passed, 2 skipped.

## AI usage

Claude Code (Claude Opus 5.5) wrote the change and the test; the change was reviewed with Claude subagents and OpenAI Codex.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * FastAPI’s automatic telemetry is disabled. Backend requests no longer generate its built-in traces, metrics, or logs.
* **Documentation**
  * Docker deployment guidance warns that setting `OTEL_PROPAGATORS` to a propagator not installed in the image can prevent backend containers from starting. Leave this setting unset unless the required propagator packages are available in the image.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac9f948ffd22`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.