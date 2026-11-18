# Issue

**Title:** RELEASE Retry on missing CCD

## Description

Issues:

- https://linear.app/metriport/issue/ENG-1198

### Dependencies

none

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

- **New Features**
  - Added automatic retry with backoff when loading metadata files, improving resiliency and reducing transient failures.
  - Metadata loading now returns paired file identifiers and contents to better track fetched items.

- **Bug Fixes**
  - Improved handling when document binary data is missing, providing clearer, more actionable error details.
  - Prevented duplicate metadata fetches, reducing unnecessary requests.
  - Strengthened validation and error reporting when no metadata is available after retries.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6fdeb28c045b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.