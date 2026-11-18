# Issue

**Title:** RELEASE FHIR Converter, XML preprocessing, unit normalization improvements

## Description

Issues:

- https://linear.app/metriport/issue/ENG-1110
- https://linear.app/metriport/issue/ENG-1337

### Description

- 
- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added ejection-fraction unit normalization so measurements display in consistent units.

* **Bug Fixes**
  * Improved handling of missing/undefined inputs to avoid runtime errors.
  * Enhanced error reporting for easier troubleshooting.

* **Tests**
  * Extended test coverage for XML character handling and null-flavor replacement scenarios.

* **Chores**
  * Updated FHIR resource statistics and added several resource type counts.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c437df5efe89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.