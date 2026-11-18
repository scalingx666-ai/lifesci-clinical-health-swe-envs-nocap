# Issue

**Title:** RELEASE better formatting of notes

## Description

Issues:

https://linear.app/metriport/issue/ENG-1109
https://linear.app/metriport/issue/ENG-1111

### Dependencies

- none

### Description

- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [x] FHIR Integration Test ran with validation
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Preserve spacing and line breaks in CDA content during conversion, improving text fidelity.
  * Maintain line breaks for Base64-encoded values to avoid unintended formatting changes.

* **Documentation**
  * Expanded usage instructions for running integration tests and monitoring progress.

* **Chores**
  * Updated integration test scripts to new locations and adjusted references to ensure they run correctly.
  * Aligned internal script paths for comparison utilities to the new directory structure.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ce328493396`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.