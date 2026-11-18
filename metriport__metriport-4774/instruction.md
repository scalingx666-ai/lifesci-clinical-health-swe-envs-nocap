# Issue

**Title:** ENG-954 new role for analytics DB s3 permissions

## Description

### Dependencies

- Upstream: 
- Downstream: none

### Description

New role for analytics DB s3 permissions - [context](https://metriport.slack.com/archives/C04FZ9859FZ/p1759186866714919?thread_ts=1759185016.192089&cid=C04FZ9859FZ)

### Testing

none

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * Standardized the IAM role name used for database-to-S3 access to align with environment conventions. No changes to functionality, permissions, or behavior. Transparent to users with no downtime or required configuration updates. Existing clusters continue operating normally; future deployments will use the updated naming. Monitoring, automation, and operational workflows remain unaffected. This is a low-risk infrastructure housekeeping update aimed at consistency and clarity in environment management.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `205aff63d595`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.