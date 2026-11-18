# Issue

**Title:** Ground form values in reviewed visual evidence

## Description

## Description
OCR reading order can attach values to the wrong repeated label or section. This change computes directional geometric associations from original source boxes, retains eligible alternatives and requires explicit association review before exporting protected field values. Unknown controls, stale approvals and conflicting field assignments block export; handwritten values additionally require a current transcription review bound to the exact selected reading.

## Type of Change
- [x] New feature
- [x] Documentation and focused regression coverage

## Changes Made
- Add bounded section, label, printed-value, handwriting and control observations with explicit layout policy, scores and abstention reasons.
- Preserve original page citations through reports and the existing review renderer; keep protected strings out of diagnostic surfaces.
- Recompute associations during all-or-nothing export and bind decisions to the complete current input and policy.

## Testing
- [x] 39 focused form controls; 177 combined tests and 26 subtests.
- [x] Full suite: 24,668 passed, 158 skipped and 11,361 subtests passed.
- [x] Canonical format, lint, format-check, type and brand checks; explicit forms-package mypy.
- [x] Public API compatibility, strict documentation build and executable synthetic guide example.
- [x] Scoped pre-commit, Bandit, secret scanning and every incoming commit's attribution policy.

## Documentation
- [x] Guide, navigation and publication registry updated.
- [x] Public API docstrings and changelog updated.

## Dependencies and Merge Order
No new third-party dependencies. This branch includes the separate prerequisites #4385 and #4396. Merge #4385, then #4396, before this PR; refresh from master and revalidate afterward. The form-grounding change is its own final commit; the current master-targeted diff includes those prerequisites so the full CI matrix runs.

This Python association/export layer does not add an OCR or handwriting model, a Swift review UI, clinical qualification or automatic clinical decisions. Recognition, section declarations and reviewer authentication remain application responsibilities.

## Related Issues

## Example
The guide executes a synthetic field/value association, explicitly confirms the reviewer choice, preserves its original box in protected output and proves the label/value strings are absent from reports.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13307eb17ea6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.