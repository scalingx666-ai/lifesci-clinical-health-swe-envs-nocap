# Issue

**Title:** feat: add fail-closed required audit receipts for declared service operations

## Description

# Pull Request

## Description
Defines fail-closed service behavior when required audit recording is unavailable. A new standalone module, `openmed/service/required_audit.py`, adds an explicit required-audit policy and a bounded, durable intent/receipt interface for declared state-changing operations. Admission, commit, and reconciliation go through the existing hash-chained action ledger. A missing or unacknowledged audit record can therefore never be reported as a fully evidenced success.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [x] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [x] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- `RequiredAuditPolicy` declares each state-changing operation with a `CommitBoundary` (`invocation` or `acknowledged`) and a bound on open receipts (default 64, max 4096). Undeclared operations are denied. Declared operations have no optional mode.
- `RequiredAuditCoordinator.perform()` appends `intent`, then `attempt`, invokes the effect once with an opaque `idem_` key, then appends `commit`. If storage is full, an append is rejected, or an acknowledgment is lost before the effect, the result is `denied`. After the effect, the result is `reconcile_required` with pending evidence. With `invocation`, an adapter failure counts as an unknown outcome. With `acknowledged`, it is recorded as `abort` and denied.
- `reconcile()` takes no effect port. A terminal record that is already durable (interrupted acknowledgment) is returned as is. An intent-only receipt is aborted. An attempted receipt is resolved through a read-only observer that uses the existing `ObservationState`. The ledger refuses a second terminal record and a failed close is re-read, so the same receipt is completed exactly once. Retrying `perform()` with the same request key never re-invokes the effect.
- `ActionLedgerAuditStore` maps stages onto the existing `ActionLedger` states (`proposed`, `attempted`, `committed`, `rejected`), so no new audit backend is added. `open_receipts()` and `reconcile_open()` rebuild receipts after a restart.
- An optional `AuditSink` (for example `HashChainAuditLog`) receives value-free outcome events on a best-effort basis. It never changes an outcome, never upgrades evidence, and cannot be installed as the required store.
- Receipts, ledger entries, diagnostics, and errors carry only fixed reason codes, opaque `rcpt_`, `act_`, and `idem_` identifiers, and `sha256:` digests. Request keys are hashed and never persisted.
- New docs page `docs/security/required-audit.md`, added to the nav and publication manifest. CHANGELOG entry added.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

Before the implementation, the new tests failed at collection with `ModuleNotFoundError: No module named 'openmed.service.required_audit'`.

- `.venv/bin/python -m pytest tests/unit/service/test_required_audit.py tests/integration/service/test_required_audit_faults.py -q`: 58 passed
- `.venv/bin/python -m pytest tests/unit/test_doctests.py tests/unit/test_docs_publication.py tests/unit/test_public_api_docstrings.py tests/unit/test_pages_manifest.py -q`: 138 passed, 2 skipped
- `.venv/bin/python -m pytest tests/unit/service tests/integration/service -q`: 790 passed, 5 skipped
- `python scripts/security/check_effect_paths.py --check`: `effect_paths_verified`
- `ruff check` and `ruff format --check` on the changed Python files: clean

The unit tests run a fault matrix over disk-full, rejected-append, and interrupted-acknowledgment faults at each stage, for both boundaries. They also cover: no blind retry, exactly-once reconciliation, restart rebuild, the open-receipt bound, idempotency conflicts, diagnostics that cannot substitute for evidence, forged receipt fields, and sentinel leak checks. The integration tests use the real ledger with an injected `ENOSPC` on entry writes and an interrupted directory sync after an entry is linked.

## Documentation
- [x] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `ruff format`, `ruff check`, and `ruff format --check` on the changed files
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Notes
- No existing service files change. `app.py`, `jobs.py`, and `logging.py` are untouched. Wiring specific routes or the job queue to the coordinator is left as a follow-up, so this PR does not overlap the open jobs-durability work in #3574.
- The commit boundary is always the effect invocation. `CommitBoundary` declares whether an adapter failure proves the effect did not commit (`acknowledged`) or leaves its outcome unknown (`invocation`).
- The action ledger reports every OS write failure as one code, so the adapter maps those to `audit_unavailable` (durability unknown), not `audit_storage_full`. Before the boundary the result is still a denial. Only the evidence field differs (`pending` instead of `none`).
- The coordinator's internal methods avoid names such as `commit`, `execute` and `send` that `scripts/security/check_effect_paths.py` treats as effect calls. It only appends to the local action ledger, and no audit-ledger path is classified in `effect_paths.json` today, so `effect_paths.json` is unchanged. The caller-supplied effect is the operation that needs classifying wherever it is wired in.
- A ledger directory holds one run, and its operations must stay declared in the policy. If the ledger names an operation the policy no longer declares, reads fail closed with `audit_read_failed`.

## Related Issues

Related to #2766, #3574, #3599, #3601

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29ffa70050cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.