# Issue

**Title:** RELEASE bulk ingestion using original s3 prefix

## Description

Issues:

- https://linear.app/metriport/issue/ENG-954

### Dependencies

none

### Description

- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this
- [ ] Manually trigger the deployment

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added a local execution mode for CSV merging via a new CLI flag, with a clear “running on local” warning.
  * Outputs are now grouped by patient using a standardized prefix for easier navigation and downstream processing.

* **Bug Fixes**
  * Normalized generated file names to remove unintended path fragments, ensuring consistent keys during upload.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8481f339a99`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.