# Issue

**Title:** feat: add offline synthetic dataset release gates

## Description

## Included pull requests

- #3625 — bounded synthetic memorization audit
- #3626 — synthetic dataset license and lineage manifests

## Issues resolved

## Maintainer integration changes

Refresh both originals from current master while preserving contributor commits. Fix report truncation so a blocking memorization signal remains represented; bind reference fingerprints to matching token-shingle and character n-gram policies. Keep rejected values and private paths out of rendered errors.

Require model provenance when a dataset declares model-generated origin, and constrain saved report license labels to canonical reviewed permissive identifiers. Existing negative test functions were expanded to reproduce and verify the repairs.

Both features operate offline on user-supplied synthetic/evaluation metadata and references. No dependencies were added.

## Validation

- Combined rehearsal: **21,029 passed, 177 skipped, 11,209 subtests** in 197.63s.
- Focused release-gate/public-API/docs cases: **146 passed, 10 subtests**.
- Canonical formatting/lint, strict docs, all 3 browser artifact-budget/analytics checks, wheel/sdist builds and packaged-source verification passed.
- [x] Exact final head `373da8b96b4234d1697711ac3bf48360518b56fa`: **21,029 passed, 177 skipped, 11,209 subtests** in 190.91s. Canonical lint/format checks, strict docs, all 3 browser budget/analytics checks, package builds and packaged-source verification passed. Hosted checks have no failures; the full local suite supplies Python validation while remaining hosted jobs run.

Feature guides, public docstrings and Unreleased changelog entries are included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa6cf54021a7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.