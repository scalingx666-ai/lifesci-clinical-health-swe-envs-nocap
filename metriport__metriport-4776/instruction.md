# Issue

**Title:** ENG-954 Fix DB roles

## Description

### Dependencies

- Upstream: 
- Downstream: none

### Description

Fix DB roles - [context](https://metriport.slack.com/archives/C04FZ9859FZ/p1759189916705169?thread_ts=1759187628.841229&cid=C04FZ9859FZ)

### Testing

none

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- Refactor
  - Introduced granular, least‑privilege S3 access for analytics data by separating import and export permissions, improving security and auditability.
- Chores
  - Updated the analytics database to use dedicated roles for S3 import and export operations.

Notes:
- No user-facing changes or downtime expected.
- Existing S3 import/export workflows continue to function as before.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2374f4d3933b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.