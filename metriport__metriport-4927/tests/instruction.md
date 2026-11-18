# Issue

**Title:** ENG-000 A grab bag of tiny fixes

## Description

### Description

- Some small fixes throughout the codebase

### Testing

- Local
  - [x] Run on some problematic XMLs
  - [x] FHIR test suite

### Release Plan
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Documentation**
  * Updated FHIR coding references (removed deprecated userSelected flags; swapped two coding system URLs) and added CarePlan to resources.

* **Bug Fixes**
  * Improved handling of missing or malformed observation units with earlier bail-out.
  * More robust XML id normalization preserving original tag structure.

* **Improvements**
  * Expanded unit normalization coverage across several measurement types.
  * Optional blacklist-based filtering for queued messages.

* **Tests**
  * Added tests for varied XML id attribute permutations.

* **Chores**
  * Removed an outdated FHIR resource-count data file.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `110199f09f33`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.