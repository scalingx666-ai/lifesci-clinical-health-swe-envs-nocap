# Issue

**Title:** feat(utils): update reconv script

## Description

### Dependencies

None

### Description

Cleanup

### Testing

na

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added support for configuring the SQS queue URL via environment variables.
  * Updated reconversion kickoff to require externally provided input file and date range (no longer uses hard-coded values). The expected start date has been updated to 2025-06-01 when provided.

* **Documentation**
  * Clarified usage around configuring the SQS queue URL.

* **Chores**
  * Reordered initialization to occur after configuration is read for more reliable startup.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d8f18f397eae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.