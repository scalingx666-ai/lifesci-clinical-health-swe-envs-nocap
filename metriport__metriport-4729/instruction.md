# Issue

**Title:** RELEASE stale link bump + reconversion script update

## Description

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

* New Features
  * Reconversion loader now enforces required inputs (file name and start date) and updates the default start date to 2025-06-01.

* Chores
  * Extended the document-query lookback window from 1 to 2 weeks across connected networks.

* Documentation
  * Added a user-facing note clarifying the SQS queue URL environment variable.

* Refactor
  * Streamlined link-processing flow for document queries by consolidating logic into a helper and asynchronous execution, improving maintainability without changing behavior.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `542150d1b4fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.