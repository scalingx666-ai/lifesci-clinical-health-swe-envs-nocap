# Issue

**Title:** ENG-1226 Lambda updates

## Description

Part of ENG-1226

### Description

- CW Document Downloader lambda to also use retries on doc downloads

### Testing

- Staging
  - [x] Rerun a DQ on a patient

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- Bug Fixes
  - Added automatic retries with backoff for server errors during document downloads, reducing intermittent failures, timeouts, and improving overall stability and success rates.
- Chores
  - Upgraded external healthcare SDK to version 8.2.0, aligning with improved error handling and reliability.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7bafaa3fd587`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.