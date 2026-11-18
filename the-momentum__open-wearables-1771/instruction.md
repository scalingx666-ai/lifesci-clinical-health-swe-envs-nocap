# Issue

**Title:** fix(backend): forward SIGTERM to workers so containers stop gracefully

## Description

## What does this change?

`worker.sh` forwards SIGTERM/SIGINT to both Celery workers and waits for each of them until it has really exited, also when more signals arrive. The container's exit code is the CPU worker's. `app.sh`, `beat.sh` and `flower.sh` `exec` their last command.

## Why?

The start scripts run as PID 1 without a signal handler, so `docker stop` never reaches uvicorn or Celery. After the grace period everything is SIGKILLed: tasks in flight are cut off and the API lifespan shutdown (`endpoint_usage.flush`) never runs.

I kept both workers in one container. Two services would be cleaner, but would change the compose file of every existing deployment. The container still lives as long as the CPU worker, and an I/O worker crash still does not stop it (that gap exists today).

Behaviour changes to know about:

- on `docker stop` the exit code is the CPU worker's (normally 0) instead of 137; Celery's warm shutdown lines and the extra `set -x` lines for `trap`/`wait` appear in the logs;
- bash 5 can lose a child's exit status when a signal interrupts `wait` at the moment the child exits; only in that case the script reports 143 (stopped by SIGTERM) instead of the real code. A worker that exits on its own keeps its code, including 127 and 255. An exact code there would need a real supervisor (tini or similar), which I left out;
- when the CPU worker dies on its own, the container now waits for the I/O worker's warm shutdown (its running tasks) instead of exiting at once;
- a stop during startup (`app.sh` migrations and seeds, `flower.sh` waiting for workers) is still not passed on, as before; the docs say so.

## How did you test this?

`docker stop` on images built from `main` and from this branch (Redis and Postgres alongside):

| Container | main | this branch |
|---|---|---|
| `worker.sh` (`-t 20`) | 20 s, exit 137, no warm shutdown | 3 s, exit 0, `worker: Warm shutdown` from both workers |
| `worker.sh`, two SIGTERMs 0.5 s apart | | 4 s, exit 0, warm shutdown of both workers |
| `beat.sh` (`-t 15`) | 16 s, exit 137 | 1 s, exit 0 |
| `app.sh` (`-t 15`) | 15 s, exit 137, no lifespan shutdown | 1 s, exit 143, `Application shutdown complete.` |

`tests/scripts/test_worker_start_script.py` runs the script with a fake `uv` that stands in for both workers (trap installed before it reports ready, configurable shutdown time and exit codes, each run in its own process group so nothing outlives a failed test). 7 tests: signal forwarding, exit status from the CPU worker (0 and non-zero), a failing I/O worker on shutdown, a second SIGTERM during a slow I/O shutdown, CPU worker exit stopping the I/O worker, I/O worker crash keeping the container up. All fail on `main`; the second-signal test also fails on the first version of this branch, which it was written for. The second-signal test sends its second SIGTERM only after the CPU worker has been reaped, so it always exercises the wait for the I/O worker. They pass on bash 3.2 (macOS) and bash 5.2 (`python:3.14-slim`), including 30 repetitions on 2 CPUs with 6 busy loops.

A race probe on bash 5.2 (the CPU worker exits on its own while SIGTERM arrives, 400 runs) gives only the worker's own code or 143; the first version of the wait loop returned 255 there.

Full backend suite: 2657 passed, 2 skipped. `shellcheck scripts/start/*.sh` is clean.

## AI usage

Claude Code (Claude Opus 5.5) wrote the change and the tests; the change was reviewed with Claude subagents and OpenAI Codex.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Improvements**
  * Backend services handle shutdown signals more reliably. Workers stop accepting new tasks and allow running tasks to finish before stopping.
  * The container’s exit status reflects the CPU worker’s result. I/O worker failures do not prevent waiting for the CPU worker to shut down.
  * Docker may terminate workers that are still running when the shutdown timeout expires. Configure a longer grace period for longer-running tasks.

* **Documentation**
  * Updated the Docker deployment guide with shutdown behavior and startup-time limitations, including cases where shutdown signals may not be forwarded during startup.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3326bcffcf9a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.