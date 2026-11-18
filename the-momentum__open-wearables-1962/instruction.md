# Issue

**Title:** chore(backend): update FastAPI telemetry comment for 0.143

## Description

## What does this change?

Updates the comment above `FastAPI(telemetry=...)` in `main.py`. No code change.

## Why?

Since  (bumped in #1922), automatic OTLP exporter setup is opt-in via `FASTAPI_OTEL_AUTO_CONFIGURE=true`. The old comment said FastAPI always sets up exporters from `OTEL_*` variables. Request traces, metrics and exception logs are still on by default, so the explicit `telemetry={...}` override stays.

## How did you test this?

Default `FastAPI()._telemetry` per version:

| fastapi | `FASTAPI_OTEL_AUTO_CONFIGURE` | tracing / metrics / logs | auto_configure |
|---|---|---|---|
| 0.142.2 | unset | True | True |
| 0.143.1 | unset | True | False |
| 0.143.1 | `true` | True | True |

## AI usage

Claude Code (Opus 5.5) to check the FastAPI changes and draft the comment.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Documentation**
  * Clarified internal notes about how OpenTelemetry configuration behaves across FastAPI versions. No user-visible behavior changed.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1977273627d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.