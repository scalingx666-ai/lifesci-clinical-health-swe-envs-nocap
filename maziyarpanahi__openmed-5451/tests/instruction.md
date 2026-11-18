# Issue

**Title:** Drain requests, streams, jobs, and accelerator workers without lost or duplicate work

## Description

. Builds on the #668 readiness and drain groundwork already on master.

This adds `openmed/service/drain.py`: one single-shot `DrainCoordinator` per `ServiceRuntime`. Participants register with it and run through four ordered phases, each bounded by the budget. Readiness drops first, then admission closes, then in-flight work finishes or reaches a declared terminal state (participants run concurrently against one deadline), then queues and servers flush, then models and devices are released. The REST lifespan in `app.py` now just calls `coordinator.drain()` and registers participants for REST/GraphQL in-flight requests (the existing `inflight` and `shutting_down` counters), NDJSON streams, OpenHIM, micro-batchers, the public job queue, SMART and bulk jobs, and tracing. The runtime itself registers the warm pool and accelerators. `create_grpc_server` joins the same coordinator through a shared `CallAdmission` gate. Other lifecycle code can call `register_drain_participant(app | runtime | coordinator, participant)`, or use `CallbackDrainParticipant` for simple hooks.

What each surface does on drain:
- REST and GraphQL: new model-backed work, including `POST /jobs`, gets `503 not_ready` with `Retry-After` and `details = {reason: "shutting_down", retryable: true, retry_after_seconds}`. `/readyz` returns the same body and `/livez` stays 200. Before this change, a job submitted after shutdown returned a 500. `ServiceShuttingDownError` maps to the same 503 and to a GraphQL `shutting_down` code. Resilience treats it as non-retryable, so it is not retried and does not open a breaker.
- NDJSON streams (`/pii/deidentify/stream`, `/pii/extract/stream`): a stream may run until the settle point near the end of the window. It then stops at its next event and ends with one `{"type":"error","error":{"code":"shutting_down",...}}` line. Buffered text that was never emitted is discarded, not flushed. A window that is still running is left to finish before the source is closed, so the model reference is released only after the work settles.
- gRPC: new unary and streaming calls get `UNAVAILABLE`/`shutting_down` with a `grpc-retry-pushback-ms` trailer while the port is still open. Calls already running may finish. Open streams end with the same status at their next event, and never send `final`. `server.stop(grace)` runs in the flush phase.
- Micro-batcher: `DynamicBatcher.drain(timeout)` dispatches queued jobs instead of cancelling them, then fails anything still queued with `BatcherClosedError`, a typed retryable error.
- Job queue: status changes now go through a compare-and-set commit fence (`LocalJobStore.update_if`). Running jobs may finish. After the settle point they stop at the next document boundary, so the last progress update is the checkpoint. At the deadline, every job still queued or running becomes `cancelled` with `error.code = "shutting_down"` and `retryable: true`, and a worker that finishes later cannot overwrite that result. Before this change, `shutdown()` left jobs that had not started in `queued` forever. Terminal webhooks sent during a drain make one attempt with no backoff.
- Warm pool: `WarmPool.close()` blocks new activations and cold loads, and unloads inactive models. A request that is still running keeps its model; when its last reference finishes, the model is unloaded.
- Accelerators: synchronization runs in a daemon thread with a bounded wait, then caches are released and compared to the baseline captured at start-up. Only runtimes already imported are touched (torch CUDA only when a context already exists, MPS, MLX), and none is imported by this code.
- Evidence: `DrainReport.to_dict()` and the new `openmed_service_draining`, `openmed_service_drain_participant_total` and `openmed_service_drain_unfinished` metrics carry only phase, participant category, outcome, counts, durations and reason codes. Category labels are pattern-checked at registration, and hook exception text is never recorded.

Breaking:
- Shutdown can now take `OPENMED_SERVICE_SHUTDOWN_DRAIN_SECONDS` (default 30) plus the new `OPENMED_SERVICE_SHUTDOWN_RELEASE_SECONDS` (default 5). Keep the termination grace period above their sum; the Helm default of 45 s already is. Both values must be finite, so `inf` and `nan` are now rejected.
- Async jobs have a new terminal status `cancelled`, with `error.code = "shutting_down"`. Clients that poll `/jobs/{id}` should treat it as terminal and resubmit.
- The REST shutdown refusal now has non-null `details` and a `Retry-After` header. The error code is still `not_ready`.
- An NDJSON stream still open at the drain deadline now ends with a `shutting_down` error line instead of being cut off.
- `DynamicBatcher.submit` after close raises `BatcherClosedError`, which subclasses `RuntimeError` and keeps the same message.

Not covered:
- Real CUDA, MPS and MLX devices. The device adapters are exercised only through fakes and the CPU placeholder, because torch and mlx are not installed in the test environment.
- Durable resume from a checkpoint. On master the queue keeps payloads in memory only, so unfinished jobs become `cancelled` and retryable, and the participant never reports `checkpointed`.
- Warm-pool generations (#3575). The fence works on model references, because generations are not on master yet.
- A standalone gRPC process entry point with its own signal handling. None exists on master, so gRPC drains when the runtime's coordinator is drained (for example from the REST lifespan) or when a host awaits `coordinator.drain()`.
- Reconciling `queued`/`running` records left by a hard crash, as opposed to a drain.

Follow-up wiring for the open PRs that touch this lifecycle:
- #5162 (streams hold their permit and drain slot until the body ends): wrap its `NDJSONStreamControls` body with `app.state.drain_streams.wrap(...)`. With `RequestWork.hold()`, `http_requests` will then also count stream bodies.
- #5066 (transactional model activation): register a participant for the release phase with a priority below 80 that blocks activation, then let the warm-pool participant release retired generations.
- #4436, #4822 and #5385 (gRPC TLS, auth and credential reload): build servers through `create_grpc_server`, or register `GrpcDrainParticipant(admission, server)`. A reload must keep the same `CallAdmission` gate.
- #5446 (durable jobs for #3574): when the cooperative cancel fires, checkpoint instead of cancelling, and return `PhaseResult(checkpointed=...)` from `JobQueueDrainParticipant`. Keep `update_if` as the fence for lease handoff.

Tests: `tests/integration/test_service_drain.py` covers ordering and single-shot drains, wedged and failing participants (bounded, with value-free evidence, deterministic over repeated runs), REST/GraphQL/jobs refusals while an accepted request commits once, batched requests that are dispatched exactly once, stream terminal events with no unsafe tail, gRPC unary and stream drains with the retry trailer, a sweep of job boundaries (admission, queue, dispatch, checkpoint, commit, callback) that asserts exactly one terminal transition per job, warm-pool and accelerator baselines, three start-drain-restart cycles, and a SIGTERM test against a real uvicorn subprocess (marked `slow`). No test asserts a wall-clock duration.

Validation: `python -m pytest tests/integration/test_service_drain.py -q` (17 passed, 14 subtests; stable over 6 repeated runs), `python -m pytest tests/ -q -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py` (27633 passed, 232 skipped, 11370 subtests passed; `test_dicom_overlays.py` is ignored because `pydicom` is not installed locally, the same on master), `python -m pytest tests/unit -k "docs or publication or mkdocs or postman or openapi or troubleshooting or rest_client"` (209 passed, 15 skipped; the strict MkDocs build is left to CI), `ruff check .` and `ruff format --check .` (clean), `python scripts/security/check_effect_paths.py --check` (`effect_paths_verified`), `mypy` (no issues).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b7a9c7130d3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.