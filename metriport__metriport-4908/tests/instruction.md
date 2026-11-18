# Issue

**Title:** ENG-000 Peek DLQ script stores unique pt IDs

## Description

### Dependencies

none

### Description

Peek DLQ script stores unique pt IDs.

### Testing

- Local
  - [x] Run script against DLQ to get pt IDs
- Staging
  - none
- Sandbox
  - none
- Production
  - none

### Metrics

none

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added CLI flags for controlling message peeking: `--max-messages` to limit results and `--download-files` to optionally download S3 files.
  * Generates deduplicated customer and patient identifier exports in CSV and JSON formats.

* **Updates**
  * Refactored message retrieval logic with improved batch processing and deduplication.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `460e02df5b95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.