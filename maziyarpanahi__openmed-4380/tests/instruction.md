# Issue

**Title:** feat: add authorized service recovery operator CLI

## Description

# Pull Request

## Description

Add a local operator CLI, `openmed service-recovery`, that exposes authorized
service recovery actions through injected component services. `inspect`,
`plan` and `verify` are read-only; `apply` runs one supported recovery action
only after the exact plan, active state generation, state digest, recovery
point and a signed single-use approval all match. The command owns only the
adapter and plan presentation; backup storage, model activation, migration
engines and job replay stay inside the injected components.

## Type of Change

- [ ] Bug fix (non-breaking change which fixes an issue)
- [x] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [x] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made

- New `openmed/cli/service_recovery.py`:
  - Commands `inspect`, `plan --action A --recovery-point REF [--output FILE]`,
    `verify --plan FILE [--approval FILE]` and
    `apply {restore-backup,rollback-model,replay-jobs} --plan FILE --approval FILE`.
  - Injected ports: `RecoveryStateService` (read-only `inspect`) and one
    `RecoveryComponentService` per action (read-only `recovery_points` and
    `propose`, compare-and-set `apply`), bundled in `ServiceRecoveryServices`
    with an existing `ApprovalTokenVerifier` and reviewer role.
  - `RecoveryPlan` commits every field in `plan_digest`; `approval_digest`
    is a domain-separated digest of the plan digest, action, active generation
    and state digest. Operators issue an existing `ApprovalToken` for it with
    `ApprovalTokenSigner` and a caller-provided HMAC key.
  - `apply` rejects before application on: unprotected or edited inputs,
    action mismatch, changed generation or state digest, unknown or
    incompatible recovery point, stale plan contents, component hold, approval
    bound to another plan or state, expired approval, bad signature or role,
    replayed nonce, and a state change after consumption.
  - Distinct exit codes: 0 ready/completed, 1 failed, 2 invalid input,
    3 denied, 4 held, 6 conflict, 7 unavailable, 8 partial. A reported
    completion that does not advance the generation by one, or a held,
    unavailable or failed result that changed state, is rejected as
    `service_result_invalid`.
  - Output is one compact JSON document of fixed codes, counts, generations,
    opaque `rp_` references and digests. Component stdout/stderr is discarded;
    argument values, paths, signatures and exception text are never echoed.
    `plan --output` creates a new `0600` file exclusively and never replaces
    an existing one.
  - Reuses the protected-file reader and receipt digest from
    `openmed/cli/governed_workflows.py` and the approval token signer,
    verifier and nonce store from `openmed/agent/approvals/tokens.py`.
- `openmed/cli/main.py`: three-line lazy registration of the help/completion
  surface. Without injected services every console command reports
  `adapter_unavailable` (exit 7); deployments call `run_service_recovery_cli`.
- New `docs/cli/service-recovery.md` with the command table, exit codes,
  approval binding order and a complete offline embedding example (executed
  by the tests); nav and publication entries; CHANGELOG entry.

## Testing

- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

New tests in `tests/unit/cli/test_service_recovery_cli.py` use synthetic fake
services, an in-memory nonce store and synthetic keys. They prove `inspect`,
`plan` and `verify` never call `apply`, never claim a nonce, leave state
unchanged and write no files (except the explicit `--output`), and that
changed state, stale approvals, stale plans and incompatible recovery points
reject before application.

```
PYTHONPATH=$PWD ../.venv/bin/python -m pytest tests/unit/cli/test_service_recovery_cli.py -q
# 37 passed
PYTHONPATH=$PWD ../.venv/bin/python -m pytest tests/unit/cli -q
# 779 passed, 298 subtests passed
PYTHONPATH=$PWD ../.venv/bin/python -m pytest tests/unit/test_doctests.py tests/unit/test_docs_publication.py tests/unit/test_public_api_docstrings.py tests/unit/test_pages_manifest.py -q
# 138 passed, 2 skipped, 32 subtests passed
python scripts/security/check_effect_paths.py --check
# effect_paths_verified
ruff check / ruff format --check on changed Python files
# All checks passed
```

## Documentation

- [x] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality

- [x] I ran `make format`, `make lint`, and `make format-check` (ran the
      equivalent `ruff format` and `ruff check` on the changed files)
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

## Dependencies

- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Notes

- The durable component services from #3574, #3575 and #3577 are not merged
  yet, so this PR defines the narrow ports they implement and tests against
  fakes. No backup, activation, migration or replay logic is added here.
- `verify` checks the approval binding and expiry but not the signature,
  because the existing verifier only verifies while atomically claiming the
  single-use nonce. The signature is verified, and the nonce claimed, only by
  `apply`.
- The console entry point has no service-loading mechanism by design (no
  ambient configuration); it mirrors the existing `openmed agents workflow`
  surface, which also requires explicit injection.

## Related Issues

Related to #3574, #3575, #3577, #3578, #3600

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29ffa70050cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.