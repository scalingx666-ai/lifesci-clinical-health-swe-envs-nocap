# Issue

**Title:** Inject disk, clock, process, network, cancellation, and corrupted-state faults into service tests

## Description

.

This adds a test-only fault-injection harness under `tests/faults/`. It comes with a versioned, seeded fault-plan schema and a value-free result-manifest schema (`openmed/core/schemas/json/service_fault_plan.schema.json` and `service_fault_manifest.schema.json`).

`tests/faults/seams.py` adds injection seams at adapter boundaries:

- disk: ENOSPC, EIO, partial write and fsync failure, limited to the case's own paths
- clock: skew, forward and backward jumps, and a stalled monotonic clock
- process kill, with restart from a crash image taken at the seam
- network: refused, timeout and reset over an in-memory transport, plus egress denied through `core/offline.py`
- cancellation at state transitions
- truncated or garbled store files

`tests/faults/runner.py` runs every case twice. The control run must pass through the seam and reach the component's baseline. The fault run must fire and reach the case's one documented outcome. The runner then writes a deterministic manifest.

The 48-case plan in `tests/faults/service_fault_plan.json` covers the components on master today:

- `LocalJobStore`
- the job queue worker and its terminal webhook
- `deliver_webhook`
- the offline socket guard
- request signing
- the circuit breaker
- the concurrency gate
- `LocalArtifactStore` and the SQLite Journey store

Later features plug into the same seams, runner and manifest. Durable jobs (#3574), model activation (#3575) and backup (#3577) each register a component in `tests/faults/scenarios.py` and add cases to the plan.

Production configuration can't turn a fault on:

- The harness is not in the wheel.
- It refuses to import under `OPENMED_PROFILE=prod`.
- It arms only under `OPENMED_PROFILE=test`.
- No env var, config key or route can enable a fault.

Tests check this against the shipped Dockerfiles, Compose defaults and Helm values.

No product code changes. Where master misses a documented outcome, the plan marks the case as a known gap, and an `xfail(strict=True)` test names the owning issue:

- #3574:
  - shutdown leaves a cancelled job `queued` (this was #3467, now part of #3574)
  - a running job that is cancelled or killed stays `running` after restart
  - a full disk in the worker strands the job
  - the job store publishes without fsync and leaves a stale temp file after a kill
- #3702: cancelling `ingest_graph` leaves the content blob orphaned

Not covered:

- Real SIGKILL and power loss. A kill is simulated by a crash image taken at the seam, so the missing fsync cannot be proven to lose data.
- Real device ENOSPC or EIO.
- Cross-component scenarios for features not on master yet: durable jobs, model activation, backup and restore, migrations, upgrades, credential reload, egress policy and audit continuity.
- Two kill rows leave files behind that no issue owns yet. The manifest records `residue_count` for them, but they are not asserted. One is the staged temp blob after a kill after `os.link`. The other is an unreferenced blob after a kill before the Journey metadata commit.

Validation:

- `pytest tests/faults -q`: 30 passed, 7 xfailed (strict), 119 subtests passed; this includes the 2 `slow` guard tests (an AST scan of the package and a subprocess import under the prod profile)
- `pytest tests/ -q -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py`: exit 0, 26151 passed, 182 skipped, 7 xfailed, 0 failed. `test_dicom_overlays.py` is ignored because `pydicom` is not installed in the local venv.
- `ruff check .` and `ruff format --check .`: clean
- `mypy`: clean (4 files)
- `scripts/security/check_effect_paths.py --check`: `effect_paths_verified`
- `scripts/release/check_repo_policy.py --commits origin/master HEAD`: passed
- docs-related unit tests (`tests/unit -k "docs or publication or mkdocs"`): 152 passed. The strict MkDocs build is left to CI; the only docs change is a new section in the existing `docs/testing.md`, so no nav change.
- `OPENMED_PROFILE=test python -m tests.faults.runner --output manifest.json`: exit 0. The same command under `OPENMED_PROFILE=prod`, or with no profile set, is refused with a fixed reason code.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7c0322f1b17`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.