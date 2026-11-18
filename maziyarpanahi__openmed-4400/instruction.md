# Issue

**Title:** Gate ambient extraction and finalization on reviewed speaker roles

## Description

## Description
A speaker alias or high-confidence role guess can incorrectly attribute patient, clinician, caregiver or interpreter statements. This change preserves explicit unknown, single-hypothesis and multiple-role states, then requires current per-span reviewer decisions before a local role-sensitive extractor receives source text. Note finalization rechecks the complete source and role context instead of trusting an earlier draft.

## Type of Change
- [x] New feature
- [x] Documentation and focused regression coverage

## Changes Made
- Keep role hypotheses, confidence and registered transcript evidence separate from acoustic aliases and prior alias-level approvals.
- Bind reviewer selection or correction to actual protected text, transcript/token/time lineage, current diarization and the complete required observation set.
- Block incomplete or stale attribution before extraction and recheck mutable context after the callback.
- Support explicitly provisional drafts while requiring refreshed finalized-source review and extraction before note finalization.
- Preserve content-free audit lineage and sanitize callback failures without exposing transcript or draft content.

## Testing
- [x] 28 focused role-gate controls; 228 combined tests and 10 subtests.
- [x] Full suite: 24,649 passed, 158 skipped and 11,361 subtests passed.
- [x] Canonical format, lint, format-check, type and brand checks; explicit ambient-package mypy.
- [x] Public API compatibility, strict documentation build and executable synthetic guide example.
- [x] Scoped pre-commit, Bandit, secret scanning and complete incoming commit attribution.

## Documentation
- [x] Guide, navigation and publication registry updated.
- [x] Public API docstrings and changelog updated.

## Dependencies and Merge Order
No new third-party dependencies. This branch preserves #4386 (speaker aliases) and #4388 (transcript lineage) through a prerequisite merge. Merge both prerequisites before this PR, then refresh from master and revalidate. The role-gating implementation is its own final commit; targeting master runs the complete CI matrix while the prerequisite diff remains visible.

This Python gate does not infer roles, load a speech/note model, authenticate a reviewer, provide a Swift UI or qualify clinical notes. Applications supply truthful cluster/span assignments, a complete required-source inventory and a trusted local extractor. Consent, de-identification, factuality and clinical review remain separate requirements; no medical record is updated.

## Related Issues

## Example
The executable guide retains competing patient/clinician hypotheses, explicitly reviews the lower-confidence patient role, invokes a synthetic local extractor with the original cited span, and finalizes a protected role-bound note while keeping source and draft strings out of reports.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aecf3a88ef5a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.