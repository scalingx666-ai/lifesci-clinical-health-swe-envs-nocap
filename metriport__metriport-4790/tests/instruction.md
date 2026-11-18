# Issue

**Title:** ENG-1198 Retry on missing CCD

## Description

Ref eng-1198



### Dependencies

none

### Description

Retry on missing CCD during the inbound flow.

### Testing

- Local
  - [x] inbound works
  - [x] inbound with missing CCD retries 8 times
- Staging
  - [x] inbound works
  - [x] inbound with missing CCD works
- Sandbox
  - none
- Production
  - none

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added automatic retrying with configurable timing to improve availability when metadata files aren’t immediately present.

* **Bug Fixes / Improvements**
  * Reduced intermittent “metadata not found” failures by accumulating partial results across attempts.
  * Enhanced error messages for document retrieval with richer context to aid troubleshooting.

* **Refactor**
  * Metadata retrieval now returns structured file entries (key + contents) for more reliable downstream processing.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1fc222d5ed28`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.