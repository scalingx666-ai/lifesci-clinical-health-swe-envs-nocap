# Issue

**Title:** feat: reconcile overlapping ASR windows with protected lineage

## Description

## Description
Reconcile fixed overlapping ASR results without duplicating shared statements or silently dropping negation. Tokens are coalesced only when their original text and stream-relative timing match across the complete overlap.

Missing, reordered, incomplete, provisional, or conflicting windows remain on hold with explicit reasons and protected original alternatives. The resulting INSERT/FINALIZE events use the existing transcript ledger. Release recomputes the exact edit plan and passes through the existing local PHI-withholding buffer; alignment success never substitutes for privacy clearance.

## Type of change
- [x] New feature
- [x] Documentation update
- [x] Test addition/improvement

## Scope and prerequisites
Eight new-scope files include the bounded reconciler, fixed synthetic fixtures, unit/integration controls, guide, navigation, publication manifest, and changelog. No new dependencies, weights, ASR engine, or alias policy are introduced. A focused existing CI repair also installs checksum-verified Trivy directly from its release, avoiding the failing installer redirect before scanning.

This branch includes prerequisite #4392 and its transcript-lineage prerequisite #4388 to validate against master while preserving history. Land those first, then refresh this branch before merging.

## Validation
- Full suite: 25,649 passed, 155 skipped, 11,361 subtests passed.
- 29 focused unit/integration controls passed on Python 3.12 and 3.11.
- Actual seam-to-ledger-to-withholding integration verifies a synthetic identifier across the overlap, retained negation, and sealed citation lineage.
- Canonical format/lint/format-check, scoped type checks, explicit module mypy, and public API compatibility passed.
- Scoped pre-commit, Bandit, and secret scanning passed.
- Strict docs/Pages build, routes, feeds, and publication metadata passed.
- Both exact guide examples executed with OS-level network denial.
- Offline wheel/sdist build, Twine, and byte-identical module-source checks passed.
- Workflow actionlint and 44 scanner/action-reference tests with 18 subtests passed for the installer repair; scoped hooks passed.
- Incoming attribution policy passed for all five commits.

## Documentation and limitations
The guide documents explicit character alignment, exact timing, stable identities, ambiguity/gap handling, buffer limits, protected alternatives, and privacy screening. Provider coverage/finality are caller-governed declarations, not recognition-accuracy evidence. Timing jitter requires review; fixed synthetic outputs do not establish clinical performance.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d62aabbd6c86`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.