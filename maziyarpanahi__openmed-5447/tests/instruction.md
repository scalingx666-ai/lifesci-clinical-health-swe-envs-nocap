# Issue

**Title:** Enforce fair bounded admission across service principals and transports

## Description

.

Adds `openmed/service/admission.py`, a transport-neutral, thread-safe `AdmissionController` with a global ceiling, per-principal ceilings and optional per-namespace ceilings (in-flight and queue at each level). Each principal has a FIFO queue, and freed capacity goes round-robin to principals with waiting work, so a waiting principal is served within `k - 1` grants to others unless its own ceiling holds it back; the queue timeout bounds every wait. Permit ownership is decided by waiter state under one lock, so cancellation, timeout and worker failure release each permit exactly once. Anonymous callers share one bucket, and principal and namespace values are stored only as process-local keyed digests.

The controller lives on `ServiceRuntime.admission_controller`, so REST and GraphQL share one budget. REST uses the `HttpAdmission` middleware, which runs after auth and inside the throttle and holds the permit until the request's tracked work settles through `RequestWork.on_finished`. GraphQL uses `RequestAdmissionExtension` in `graphql_schema.py`: each `analyze`, `deidentify` or `journeyResources` field, aliases included, takes one unit. `acquire_blocking`/`admit_blocking`, together with `grpc_status` and `grpc_trailing_metadata()`, is the adapter a gRPC interceptor can call.

Rejections carry no values: 429 `admission_limited` (`principal_limit`/`namespace_limit`) or 503 `admission_saturated` (`global_limit`), with a constant `Retry-After` and `details` of `{reason, retry_after_seconds}` only. GraphQL returns the same status and header with a single `OPENMED_ADMISSION_REJECTED` error and no partial data. The new `openmed_service_principal_admission_*` gauges and the rejection counter (labelled by reason and transport) carry no identifiers. Both error codes are registered in `api_compatibility.py`. Behaviour is documented in `docs/serving/fair-admission.md`, which is added to the nav and to `publication.yml`. Request admission is separate from async job admission (#5206) and from the throttle's proxy-aware keys (#4142). It keys on the authenticated principal, not on peer or `X-Forwarded-For`.

Fair admission is off unless an `OPENMED_SERVICE_ADMISSION_*_MAX_CONCURRENCY` ceiling is set, so existing deployments behave as before.

Not covered: the bundled gRPC server is not wired. On master it does not authenticate callers, so there is no principal to key on. Calling the blocking adapter from the gRPC security interceptor is a follow-up for #4822. Counters are per process (per replica) and are not distributed. Streaming endpoints hold their unit only until the stream response starts, the same as the existing throttle concurrency gate.

Validation: `pytest tests/unit/service/test_fair_admission.py tests/integration/service/test_fair_admission_transports.py -q` (32 passed), `pytest tests/unit/service -q` (797 passed, 5 skipped), `pytest tests/unit -k "docs or publication or mkdocs" -q` (152 passed, 15 skipped), `ruff check .` and `ruff format --check .` (clean), `python scripts/security/check_effect_paths.py --check` (effect_paths_verified), `mypy` (scoped config, no issues), `pytest tests/ -q -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py` (27649 passed, 232 skipped, 298 deselected; the ignored module cannot be collected in the shared venv because `pydicom` is not installed). `python scripts/release/check_repo_policy.py --commits origin/master HEAD` (passed). The strict MkDocs build is left to CI because `mkdocs` is not installed locally.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b7a9c7130d3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.