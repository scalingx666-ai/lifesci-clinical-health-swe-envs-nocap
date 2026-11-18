# Issue

**Title:** feat: reconcile restored approvals and authority under a new recovery epoch

## Description

# Pull Request

## Description
Adds an explicit anti-replay reconciliation boundary between backup restore and admission. A restored generation is bound to a new recovery epoch, every pre-restore approval nonce is burned in the live nonce store, recorded authority is rechecked against current injected status, and resumable effects are reconciled by idempotency key. Spent, revoked or expired authority cannot be revived by an older snapshot; unavailable authority keeps work held; committed effects are never erased and review is never claimed as repeated.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [x] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [x] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- New `openmed/agent/approvals/restore_reconciliation.py` (standalone, not re-exported from `openmed.agent.approvals` to avoid an import cycle with `openmed.agent.permissions`):
  - `RestoredSnapshot`, `RestoredApproval` (digest-only, built with `RestoredApproval.from_token`), `RestoredWorkflow` (validated lineage or `RetiredJournalRecord` plus the recorded `AuthorityBinding`).
  - `RecoveryEpochStore` protocol, `InMemoryRecoveryEpochStore`, digest-bound `RecoveryEpoch`, `epoch_action_digest` and `require_current_epoch`.
  - `RestoreReconciler.reconcile(snapshot, observe=...)`: opens a strictly higher epoch, claims each unexpired snapshot nonce in the live `ApprovalNonceStore`, checks each recorded binding with `AuthorityRuntime.check(..., AuthorityBoundary.RESUME)` before any sink read, then runs the existing `recover_workflow` planner.
  - `RestoreReconciliationReport`: deterministic canonical JSON with controlled reason codes, counts, opaque action ids, idempotency keys and digests; `require_complete()` refuses admission while anything is held.
- Dispositions: approvals `invalidated` or `held`; workflows `resume`, `complete`, `retired`, `fresh_review_required`, `review_required` or `held`.
- Pre-restore approval receipts never authorize a retry: approval-gated retries become `fresh_review_required` (`pre_restore_approval_invalidated`) and the receipt digest is kept only as `historical_approval_receipt_digest`.
- Revoked, expired, changed-generation, rolled-back and mismatched authority map to `fresh_review_required`; unavailable, stale or store-unavailable status, a missing runtime, or a failed sink lookup map to `held`.
- New docs page `docs/agent/restore-authority-reconciliation.md` with an executed example; nav, publication inventory and governance overview entries.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

Commands:

```text
.venv/bin/python -m pytest tests/unit/agent/approvals/test_restore_reconciliation.py tests/integration/agent/test_restore_authority_reconciliation.py -q
# 41 passed
.venv/bin/python -m pytest tests/unit/test_doctests.py tests/unit/test_docs_publication.py tests/unit/test_public_api_docstrings.py tests/unit/test_pages_manifest.py -q
# 139 passed, 2 skipped, 32 subtests passed
.venv/bin/python -m pytest tests/unit/agent/approvals tests/unit/agent/workflows tests/unit/agent/permissions tests/integration/agent -q
# 479 passed, 1 skipped, 507 subtests passed
python scripts/security/check_effect_paths.py --check
# effect_paths_verified
ruff check <changed python files>; ruff format --check <changed python files>
# All checks passed; 3 files already formatted
```

Acceptance coverage:
- Backup before consumption: the integration test copies a `SQLiteApprovalNonceStore` file before a token is spent, consumes it, restores the copy, and shows (negative control) that the restored file alone would accept the replay; after reconciliation a fresh verifier over the same file raises `ApprovalReplayError`. A token issued after the backup and absent from the snapshot fails against `epoch_action_digest` as an action mismatch.
- Revoked or expired authority recorded as active in the snapshot binding stays unusable (`authority_revoked`, `authority_expired`, `authority_generation_changed`, `authority_status_rollback`) and the sink is never read.
- Unavailable authority or effect status keeps work `held`, `require_complete()` raises `restore_reconciliation_incomplete`; committed effects recorded in the snapshot remain in the report, post-backup commits are reconciled and not retried, journals and sinks are unchanged, and the report contains no approval-success code.
- Sentinel tests confirm provider, store and clock exception text never reaches errors or reports.

## Documentation
- [x] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check` (equivalent Ruff commands on changed files)
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Notes
- Scope is reconciliation only: no backup format, encryption, identity service or durable epoch backend. `InMemoryRecoveryEpochStore` is single-process; production needs an injected durable epoch store kept outside every backup, mirroring the existing generation-store guidance.
- Tokens issued after a backup and not listed in the snapshot are covered only when hosts issue and verify approvals against `epoch_action_digest`.
- Burning a nonce only reduces authority, so it is applied regardless of whether the live store is itself a restored copy. Reconciliation is idempotent; rerunning opens a newer epoch and reports `pre_restore_nonce_already_claimed`.
- No existing public API changes. Python only; no Swift counterpart is introduced.

## Related Issues

Related to #2768, #3199, #3577, #3599

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29ffa70050cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.