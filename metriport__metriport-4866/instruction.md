# Issue

**Title:** Add an alert to roster generation

## Description

Part of ENG-000

_[Release PRs:]_

### Dependencies
None

### Description
Add an alert to roster generation if roster size is 0.

### Testing
- Staging
  - [x] Run roster generation on an hie with no subscribers and see if error pops up.
  - [x] Run roster generation on an hie with subscribers (no error should pop up)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Enhanced roster analytics now collects additional context per customer to improve reporting accuracy.

* **Bug Fixes**
  * Added a runtime safeguard that detects zero roster sizes and logs an error with contextual details to reduce silent failures.

* **Chores**
  * Improved internal notification and logging around roster analytics to aid faster diagnosis and monitoring.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0c985d50630a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.