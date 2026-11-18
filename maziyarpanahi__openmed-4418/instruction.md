# Issue

**Title:** feat: enforce ambient consent and capture lifecycle in Python and Swift

## Description

Ambient capture now requires consent from every declared participant under a bounded local policy. Python and OpenMedKit expose equivalent visible capture states, explicit interruption/resume, an original session deadline and revocable references for owned audio, transcript, cache and draft buffers. Withdrawal, participant changes, expiry and deletion overwrite owned data and invalidate its references.

Type: new feature.

Review export requires explicit policy opt-in and stopped capture. Exported non-audio copies always remain drafts requiring review, and their escape from session ownership prevents a later claim of complete deletion. Cleanup receipts cover owned-memory overwrite only; the host still controls microphone/model producers, caller copies and external files. This component neither makes recording-law determinations nor replaces PHI, speaker-role or clinical note review.

## Validation

- Final full Python suite: 25,810 passed, 155 skipped, 11,361 subtests.
- Focused streaming checks: 358 passed; new session controls: 20 passed on Python 3.12 and Python 3.11.
- Full Swift package: 165 tests, 17 skipped, zero failures; nine new consent/lifecycle tests passed.
- Canonical Python and Swift formatting/lint, explicit module mypy, public API compatibility, reviewed effect inventory, scoped pre-commit and actionlint passed.
- Strict documentation/site validation and the synthetic Python guide example passed.
- Frozen development install, dependency security audit, wheel/sdist build, exact packaged-source verification and Twine checks passed.
- Complete incoming commit attribution policy: passed for all 12 commits.

Python and Swift replay the same content-free transition fixture and compare complete serialized state after both accepted and refused actions. Additional controls exercise actual overwrite, stale and foreign references, expired/invalid clocks, resource limits, callback failure, export accounting and terminal timer cleanup. The guide includes executable synthetic Python usage and OpenMedKit integration examples.

## Scope and dependencies

No runtime dependencies were added. The Swift workflow now runs when the shared fixture changes. The effect inventory classifies the context manager's local cleanup call. The vulnerability workflow installs the pinned scanner directly from its release and verifies its checksum; database updates, scan commands and severity gates are unchanged. The focused vulnerability-gate checks passed: 35 tests and 11 subtests.

This branch preserves #4401 and #4402, including their speaker-alias, transcript-lineage, withholding and role-review prerequisites. Land those prerequisites first, then refresh and recheck this PR before merging. Documentation, navigation, synthetic parity fixtures and the Unreleased entry are included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7feeaa9bbbf7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.