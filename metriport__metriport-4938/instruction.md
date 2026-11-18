# Issue

**Title:** RELEASE athena projection tables

## Description

Issues:

- https://linear.app/metriport/issue/ENG-4652

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

* **Chores**
  * Infrastructure now provisions multiple partition-projected debug tables for parsed responses, created alongside existing parsed-response storage.
  * Adds per-key partition projection (date, client ID, patient ID, stage) to improve query performance, partitioned debugging, and troubleshooting of parsed response data.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18a74f3f084f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.