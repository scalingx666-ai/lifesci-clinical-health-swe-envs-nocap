# Issue

**Title:** ENG-000 Improve reconversion-kickoff script

## Description

### Dependencies

none

### Description

`reconversion-kickoff-loader` checks cxId, faster, and retries.

### Testing

none

- Local
  - [x] Sends messages to staging w/o any errors, two instances running in parallel
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

* **Enhancements**
  * Improved reliability of message queue operations with automatic retry logic
  * More frequent progress reporting during batch processing
  * Enhanced error tracking and reporting with elapsed time metrics
  * Better validation and error messages for failed payloads

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `be61906cb7e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.