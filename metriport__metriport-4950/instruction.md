# Issue

**Title:** feat(core): treat nonstring unit as missing

## Description

### Description

aborts unit normalization if unit is not of type string. shouldn't happen, but sometimes our conversion is wrong and at least this avoids failing the conversion.

### Testing

None

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Improved observation unit validation to properly reject invalid data types, ensuring more reliable data processing.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1c8b91897d7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.