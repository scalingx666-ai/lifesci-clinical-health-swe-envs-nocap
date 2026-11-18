# Issue

**Title:** fix(backend): run list_users handler in threadpool again

## Description

## What does this change?

`GET /api/v1/users` is a plain `def` handler again, so FastAPI runs it in the threadpool and it no longer blocks the event loop.

## Why?

#623 (the fix for #571) changed `list_users` from `async def` to `def`. A few days later the schema directory refactor in #560 brought `async def` back, most likely while resolving a merge conflict. Since then, every call to this endpoint has run its synchronous DB query and serialization on the event loop. The API runs as a single uvicorn process, so while that query runs no other request is handled, including provider webhooks and health checks. This is the same failure mode as #571.

I checked the other routes: this is the only `async def` handler that still takes the sync `DbSession`.

Relates to #571

## How did you test this?

Ran two API containers side by side against the same local Postgres (300k seeded users): one on `main`, one on this branch. Loaded each with N concurrent loops of `GET /users?search=example&limit=100` for 15 s while probing a trivial endpoint (`GET /api/v1/oura/webhooks/health`) every 100 ms.

| concurrent `/users` loops | `/users` req/s (main → fix) | probe p50 (main → fix) | probe p95 (main → fix) |
|---|---|---|---|
| 0 | - | 8 ms → 9 ms | 11 ms → 12 ms |
| 1 | 9.4 → 10.3 | 89 ms → 3 ms | 113 ms → 6 ms |
| 10 | 11.3 → 20.2 | 1008 ms → 6 ms | 1605 ms → 31 ms |

On `main`, unrelated requests wait for every in-flight `/users` call. With the fix they don't, and `/users` throughput roughly doubles under concurrency.

## AI usage

Claude Code (Opus 5.5): traced when the regression came back and wrote the load script.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Refactor**
  * Updated the user-listing endpoint to handle requests synchronously.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7bc4e11afd2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.