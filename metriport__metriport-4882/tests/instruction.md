# Issue

**Title:** remove unneeded DOA extension

## Description

Part of ENG-1089

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1089

### Dependencies
None

### Description
Stop sending the DOA extension to CQ.

### Testing
- Staging
  - [x] Create a CQ facility
  - [x] update a CQ facility
- Production
  - [ ] Create the failing facility

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Refactor**
  * Streamlined organization template generation by removing legacy conditional logic and feature flag evaluations. Code structure simplified with no changes to public-facing functionality.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ad5ff16941b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.