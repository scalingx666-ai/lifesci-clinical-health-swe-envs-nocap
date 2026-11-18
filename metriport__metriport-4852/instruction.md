# Issue

**Title:** PATCH RELEASE Revert change for XML preprocessing

## Description

Part of ENG-000

### Description

- Reverting changes re XML preprocessing introduced in this PR:
- 

### Release Plan

- :warning: Points to `master`
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Standardized XML parsing and building behavior, which may change element order and whitespace in generated outputs.
  * Ensures more consistent XML-to-JSON and JSON-to-XML conversions across environments.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2a0e60771d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.