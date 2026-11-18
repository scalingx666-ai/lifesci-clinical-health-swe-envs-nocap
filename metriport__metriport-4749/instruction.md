# Issue

**Title:** RELEASE athena writeback extensions

## Description

Issues:

- https://linear.app/metriport/issue/ENG-1140

### Description

- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- New Features
  - Medication and allergen searches now support name-based fallback when codes are missing.

- Improvements
  - Clearer display names derived from coding or provided text.
  - Smarter allergy reaction handling with deduplication and omission when empty.
  - Enriched search/add payloads include both codes and text for better matching.

- Bug Fixes
  - More specific errors when identifiers or display text are unavailable.
  - Early, consistent errors when write-back isn’t enabled or supported.
  - Validation restricts write-back to supported EHRs, preventing unsupported attempts.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbbb1b6242a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.