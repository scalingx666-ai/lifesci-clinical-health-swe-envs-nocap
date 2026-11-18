# Issue

**Title:** ENG-000 Log pt IDs w/o consolidated on snowflake script

## Description

### Dependencies

none

### Description

Log pt IDs w/o consolidated on snowflake script.

### Testing

- Local
  - [x] Run script w/ cx that has pts w/o consolidated and get those IDS on console
- Staging
  - none
- Sandbox
  - none
- Production
  - none

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * Added enhanced diagnostic logging during CSV generation from FHIR data. Each run now reports the count and list of patient IDs excluded due to missing consolidated data, improving observability and troubleshooting.
  * No changes to processing logic or output format; this update is log-only and does not affect results or performance.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f973e8b579a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.