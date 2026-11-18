# Issue

**Title:** ENG-954 Allow analytics DB to read/write from/to S3

## Description

### Dependencies

none

### Description

Allow analytics DB to read/write from/to S3.

### Testing

- Local
  - none
- Staging
  - [ ] ~~PG can read from S3~~ To be done on a later time, not being used in prod
  - [x] PG can write to S3
- Sandbox
  - none
- Production
  - none

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Database now supports direct import/export to the analytics S3 bucket for bulk data loads and exports.
  * Database is granted role-based access to perform object and multipart upload/download operations against the analytics bucket, improving large-transfer reliability.
  * Analytics storage access (read/write) is propagated to relevant components, enabling smoother FHIR-to-CSV and other analytics workflows.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ffecb0bc084`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.