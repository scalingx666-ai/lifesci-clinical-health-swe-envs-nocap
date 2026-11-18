# Issue

**Title:** ENG-589 CW Directory rebuilder - automated

## Description

Part of ENG-589

### Dependencies

- Upstream:  

### Description
- Added a scheduled lambda for CW Directory rebuilding to Lambdas nested stack 
- Added heartbeat ping to CW Dir rebuilding logic
- Moved CQ Directory rebuilder lambda to Lambdas nested stack

### Testing

- Staging
  - [ ] Check that the lambda exists
    - [ ] Rig the schedule on the UI and get it to rebuild CW dir 
- Production
  - [ ] Check that the lambda exists
    - [ ] Check tomorrow to see if the rebuild was successful

### Release Plan

- [ ] Upstream dependencies are met/released
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Safe heartbeat sending after CW directory rebuilds.
  * Enabled scheduled tasks for roster upload/download and for CW/CQ directory rebuilders.

* **Chores**
  * Infrastructure updated to support scheduled rebuilder lambdas and Quest tasks.
  * Configuration extended to accept rebuilder schedules and optional heartbeat URLs; service environments now include heartbeat settings.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24424cfc41c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.