# Issue

**Title:** ENG-954 Don't require job ID on bulk ingestion

## Description

### Dependencies

- none

### Description

Don't require job ID on bulk ingestion  - [contex](https://metriport.slack.com/archives/C04T5Q9JHFX/p1759192735164669)

### Testing

- Local
  - none
- Staging
  - [x] bulk ingestion on Snowflake works
- Sandbox
  - none
- Production
  - none

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- Refactor
  - Removed jobId from request handling, logs, and error messages; only cxId and patientId are used. Results in leaner payloads and consistent identifiers across processing.

- Chores
  - Updated input validation to drop the jobId field from the schema, aligning checks with the revised payload.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a677cf06704`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.