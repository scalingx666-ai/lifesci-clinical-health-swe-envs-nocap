# Issue

**Title:** ENG-1230 HIE Directory Entry View migration fix

## Description

Part of ENG-1275

### Description

- Added a default OID for `managing_organization_id` field on the HIE directory view migration
### Testing

- Local
  - [x] Migrate up and down a couple times

### Release Plan

- :warning: This contains a DB migration
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Directory view updated so the first branch now uses a fixed organization identifier for consistent directory results; the second branch remains unchanged.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `74921d062c5d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.