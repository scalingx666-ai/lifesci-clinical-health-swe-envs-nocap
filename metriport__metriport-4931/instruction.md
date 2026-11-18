# Issue

**Title:** RELEASE Some minor fixes

## Description

Issues:

- https://linear.app/metriport/issue/ENG-000
- https://linear.app/metriport/issue/ENG-1306

### Description

- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Documentation**
  * Added FHIR CarePlan resource documentation.

* **Bug Fixes**
  * Improved medical data conversion with better handling of edge cases and malformed attributes.
  * Enhanced clinical unit normalization with expanded unit mappings and null value protection.

* **Tests**
  * Added comprehensive test coverage for data conversion edge case scenarios.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5000b3e25ab6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.