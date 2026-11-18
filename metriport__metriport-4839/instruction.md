# Issue

**Title:** ENG-1226 Update CW retry logic

## Description

Part of ENG-1226

### Description
- API creates CommonWell API with options for retries
- Removed SDK retries on the linking methods because those require custom logic 

### Testing
- Local
  - [x] Run some queries with retries for CW
- Staging
  - [x] Link an existing patient
  - [x] Query docs
- Production
  - [ ] Rerun some patient create for those patients who failed

### Release Plan

- [ ] Release NPM packages (`minor` update to the Commonwell-SDK package)
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Automatic retries for server (500) errors with capped attempts and initial delay, improving resiliency for CommonWell integrations.

* **Refactor**
  * Consolidated retry behavior into a shared client layer and removed redundant per-client retry paths, simplifying maintenance while preserving normal success flows.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a03a9e0b502c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.