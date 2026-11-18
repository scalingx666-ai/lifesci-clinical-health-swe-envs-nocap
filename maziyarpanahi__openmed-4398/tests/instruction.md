# Issue

**Title:** Route OCR and VLM disagreements to bounded evidence review

## Description

## Description
OCR and VLM readings can disagree about the same field even when one answer has high confidence. This change compares original observations using explicit field/source identities, geometry, normalized text, declared semantic types and confidence. Conflicts retain both visual citations and require review; permitted agreements retain one original string unchanged, selected by an explicit policy rather than confidence or fluency.

## Type of Change
- [x] New feature
- [x] Documentation and focused regression coverage

## Changes Made
- Add bounded immutable OCR/VLM observations, explicit agreement permissions and deterministic disagreement classes.
- Retain every unresolved comparison in a bounded review queue; overflow fails closed instead of dropping conflicts.
- Integrate blocking review packets with original citation mappings and value-free reports.
- Freshly verify the entire batch before preparing agreement data. Any unresolved comparison prevents partial output; handwritten observations always remain review-required.

## Testing
- [x] 30 focused arbitration controls; 167 combined tests and 10 subtests.
- [x] Full suite: 24,698 passed, 158 skipped and 11,361 subtests passed.
- [x] Canonical format, lint, format-check, type and brand checks; explicit arbitration-package mypy.
- [x] Public API compatibility, strict documentation build and executable synthetic guide example.
- [x] Scoped pre-commit, Bandit, secret scanning and complete incoming commit attribution.

## Documentation
- [x] Guide, navigation and publication registry updated.
- [x] Public API docstrings and changelog updated.

## Dependencies and Merge Order
No new third-party dependencies. This branch includes the separate prerequisites #4385, #4396 and #4397. Merge them in that order before this PR, then refresh from master and revalidate. The arbitration implementation is its own final commit; targeting master runs the full CI matrix while the prerequisites remain visible in the cumulative diff.

Agreement is not clinical verification. Recognition, explicit field pairing and policy qualification remain upstream responsibilities. This Python routing layer does not replace transcription, form-association, privacy or clinical review gates and does not add a model or Swift UI.

## Related Issues

## Example
The executable guide accepts an explicitly permitted whitespace-normalized agreement while retaining the original OCR spacing, then routes a conflicting VLM reading to review with both original page citations and no selected value.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2672dddc2361`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.