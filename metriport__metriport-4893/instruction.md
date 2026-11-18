# Issue

**Title:** PATCH RELEASE Minor fixes for FHIR Normalization

## Description

Part of ENG-1315



Issues:

- https://linear.app/metriport/issue/ENG-1315

### Description

- Added standard unit for A1c as a recognized unit.. Can't believe it was missing 🤦‍♂️ 
- Improved logging/error reporting for unknown units

### Testing
- [x] Tested locally on normalization script 

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Improved error handling and diagnostics for unmapped observation units with detailed logging information.
  * Enhanced stability when processing observations with non-standard units.
  * Added support for percentage unit normalization in A1C measurements.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bef6bb67581d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.