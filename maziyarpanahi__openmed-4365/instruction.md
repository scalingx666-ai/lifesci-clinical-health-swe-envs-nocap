# Issue

**Title:** feat: recheck authorization for queued service work and long-lived streams

## Description

# Pull Request

## Description
Authentication decides whether a request is admitted, but a queued job or a long-lived stream can keep running after the consent, scope or policy revision it was admitted under has been revoked or has expired. This PR adds `openmed.service.continuation_auth`, an injectable guard that binds admitted work to an authorization epoch and checks it again before each protected output, each resume, each effect dispatch and each declared checkpoint.

When authority has expired or been revoked, or the work is cancelled, the guard stops the work. For integrity or availability failures it quarantines the work. In both cases it closes the epoch and returns an explicit, content-free reconciliation outcome. Committed effects are reported as committed and are never claimed to be undone. Buffered output is discarded, not released.

The module covers continuation authorization only. Identity policy and the durable queue are out of scope. It reuses existing primitives: `AuthorityRuntime` / `AuthorityBinding` (status provider, monotonic generation store, trusted clock), `EffectRecord` / `EffectState` for effects, and `CancellationSignal` for cooperative stops. `jobs.py`, `streaming.py`, `auth.py` and `app.py` are not modified.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [x] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [x] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- `openmed/service/continuation_auth.py` (new):
  - `ContinuationGuard.admit` pins current authority generations into a persistable `ContinuationRecord`. The record holds a random admission id, a work-id digest, the declared checkpoints and the authority binding. It never stores a verdict, and `from_dict` rejects extra fields.
  - `check` / `require` / `cancel` look up fresh status at the `execution_start`, `resume`, `checkpoint`, `effect_dispatch` and `protected_output` boundaries.
  - Dispositions are `continue`, `completed`, `stopped` and `quarantined`. Every non-continue decision closes the epoch in an injected `ContinuationLedger`, so it can never continue again (`continuation_terminal`).
- `run_continuation` runs queued work with a `ContinuationContext`:
  - `checkpoint(name)` checks a declared checkpoint.
  - `commit_effect(effect, dispatch)` checks first, records the effect as pending, and marks it committed only when the dispatch returns valid evidence.
  - `emit(output)` buffers output, which is released only after a final protected-output check.
  - A worker exception becomes a `continuation_worker_failed` quarantine, with no message or traceback kept.
- `GuardedStream` wraps sync or async sources. It checks before reading the source and again before each chunk, always closes the source, and records disconnect or task cancellation as `continuation_cancelled`. It optionally ends with `continuation_error_event`, which matches the shape of the existing NDJSON error envelope.
- `principal_authority` / `consent_authority` derive `AuthorityContract`s. The principal contract commits to subject, credential type, key id, scopes and policy revision; the consent contract is referenced by its digest.
- Outcomes report `committed_effect_count`, `pending_effect_count`, a committed-effect digest, a `reconciliation` state (`no_effects`, `committed_effects_retained`, `pending_effects_unconfirmed`) and a fixed `"compensation": "not_attempted"`.
- Docs page `docs/serving/continuation-authorization.md`, plus nav, publication inventory and CHANGELOG entries.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

Before the change, the new test modules failed at collection with `ModuleNotFoundError: No module named 'openmed.service.continuation_auth'`. As a mutation check, removing the runtime recheck inside the guard makes 19 of the new tests fail.

```bash
PYTHONPATH=$PWD python -m pytest tests/unit/service/test_continuation_auth.py tests/integration/service/test_continuation_authorization_flow.py -q
# 36 passed
PYTHONPATH=$PWD python -m pytest tests/unit/service tests/integration/service tests/unit/agent/permissions -q
# 901 passed, 6 skipped, 433 subtests passed
PYTHONPATH=$PWD python -m pytest tests/unit/test_doctests.py tests/unit/test_docs_publication.py tests/unit/test_public_api_docstrings.py tests/unit/test_pages_manifest.py -q
# 138 passed, 2 skipped, 32 subtests passed
python scripts/security/check_effect_paths.py --check
# effect_paths_verified
ruff check <changed files> && ruff format --check <changed files>
# All checks passed; 4 files already formatted
```

The acceptance criteria are covered by these tests:
- **Revocation after admission:** revoking synthetic authority stops later stream chunks (sync, async and NDJSON) and queued execution, whether before pickup, at a checkpoint, before an effect, or at the final output release.
- **Restart cannot revive consent:**
  - A restarted worker with a fresh generation store and ledger still sees the revocation.
  - Re-pinning the restored generations is rejected.
  - Cached `authorized`/`status` fields are rejected.
  - A durable ledger keeps cancelled or quarantined epochs closed after the job row is reset to `queued`.
  - A durable generation store detects a provider rollback.
- **Honest effects and no leaks:** committed effects remain recorded with `compensation: not_attempted`, ambiguous dispatches are reported as pending/unconfirmed, and buffered output is withheld. Sentinel values do not appear in outcomes, records, errors, tracebacks or the persisted job file.

## Documentation
- [x] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check` (equivalent `ruff format` / `ruff check` on the changed files)
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Notes
- This PR does not wire the guard into `openmed/service/jobs.py` or `/pii/deidentify/stream`. Several open PRs edit those files, so the guard ships as an injectable component; the docs page states this. Wiring can follow once those PRs land.
- Status lookups reuse `AuthorityRuntime`. `AuthorityKind` and `AuthorityBoundary` are unchanged. Service boundaries map onto the existing ones: execution start, resume and checkpoint map to `resume`; effect dispatch maps to `effect_dispatch`; protected output maps to `sensitive_read`. Service principals map to `grant` contracts and consent to `purpose_ticket` contracts.
- Expired, revoked and cancelled work is `stopped`. Stale or unavailable status, generation changes or rollback, contract or work mismatch, undeclared checkpoints, worker or source failures and ledger failures are `quarantined`. Both close the epoch, and a new admission creates a new epoch.
- `InMemoryContinuationLedger` covers a single process. For restart safety, production needs a durable ledger and generation store kept separately from job metadata (documented).

## Related Issues

Related to #3549, #3574, #3576

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29ffa70050cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.