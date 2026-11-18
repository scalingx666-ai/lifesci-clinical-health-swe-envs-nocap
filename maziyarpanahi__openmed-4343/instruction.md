# Issue

**Title:** fix: renew expired repository governance reviews

## Description

## Description
At the October 30 date rollover, the shared claims and brand review deadlines expired and started failing unrelated v3.2 PR validation. Recheck the repository-derived contracts and renew their review window through November 30.

## Type of Change
- [x] Bug fix
- [x] Documentation update

## Changes Made
- Refresh the canonical offline claims review date and include it in the generated snapshot date.
- Preserve every claim value, status, qualification and public wording. All six unsupported claims remain unverified with no publishable value or wording.
- Preserve observation dates and deadlines for the external community/GitHub evidence and model snapshot.
- Renew the seven existing site-role reviews and system deadline, retaining their guardrails and recording the review in the brand changelog.
- Refresh only the claims input checksum in the social manifest; approved assets, homepage HTML and its analytics exception are byte-identical.

## Testing
- [x] 25 focused brand/language-coherence checks.
- [x] Canonical format, lint and format-check.
- [x] Exact head `61e72eb3c2d6ac731e8270e34f076e747df7fae7`: 21,327 passed, 177 skipped, 11,209 subtests passed in 181.75s.
- [x] Strict docs and all three Chromium budget/homepage-beacon/clinical-exclusion guards passed.
- [x] Canonical social manifest reproduction passes with unchanged approved assets.

Master has no required hosted status contexts. Hosted checks were reviewed for failures; the complete exact-head local suite and relevant source/documentation gates cover this prerequisite.

No validator or test is skipped or weakened. No network evidence refresh or external profile action is performed.

## Related Issues
Related to #3195.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34914b567cb2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.