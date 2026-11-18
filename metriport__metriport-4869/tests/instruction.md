# Issue

**Title:** fix(core): add capture.init to the roster upload lambdas.....

## Description

Part of ENG-000

_[Release PRs:]_

### Dependencies
None

### Description
...... add capture.init....
### Testing
- Local
  - [x] Make sure message appears locally
- Staging
-  [ ] Make sure message appears if roster size is 0
-  [ ] Make sure message does not appear if roster size is not 0

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Refactor**
  * Streamlined error handling for empty roster scenarios, standardizing messages and metadata while maintaining existing behavior.

* **Chores**
  * Ensured telemetry/error reporting initializes at startup for the roster processing service, improving reliability of diagnostics and monitoring.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae359097422b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.