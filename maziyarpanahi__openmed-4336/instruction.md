# Issue

**Title:** feat: add offline locale readiness and conformance tools

## Description

Add offline tools for contributors and release reviewers to inspect language-pack readiness and conformance. Readiness matrices distinguish complete, partial, blocked and missing-evidence capabilities; the CLI reports each pack component independently without loading a model or contacting the network.

## Included pull requests

- #3617 — deterministic language readiness JSON/Markdown matrices.
- #3619 — `openmed i18n check` with independent metadata, registry, validator, surrogate, fixture, span and evidence results.

## Issues resolved

## Maintainer integration changes

- Update both branches from current master and retain current CI policy and published release history.
- Require a real installed surrogate backend or supported conceptual fallback; a valid tag alone cannot pass conformance.
- Omit rejected provider/locale values, fixture safety declarations and span labels from diagnostic details. Five existing negative cases reproduced the value echoes before the repair; the successful golden output and reason codes remain stable.
- Reconcile the shared Unreleased notes. The real integration tree matches the passing rehearsal exactly.

## Validation

- Full suite on final head `16fbd269652bec3bdc904d16386e61adaf74c573`: 20,671 passed, 177 skipped, 11,209 subtests passed in 173.28 seconds (`.venv/bin/python -m pytest tests/ -q -n 8 --tb=short --show-capture=no`). The complete rehearsal run also passed.
- Focused readiness/CLI checks: 259 passed, 3 subtests passed. The final original’s integrated CLI/matrix checks also pass (84 tests).
- `make format`, `make lint`, `make format-check`, strict docs staging and the browser artifact-budget/analytics guards passed.
- Final-head docs and wheel/source builds passed; both new modules are present in the wheel with matching source hashes. The fixed artifact budget and protected homepage/clinical analytics checks pass (3 browser checks).

No dependencies or model assets are added. These are declaration/wiring checks and do not certify clinical language quality.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd76e8c7fb9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.