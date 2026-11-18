# Issue

**Title:** Remove early return if roster is empty

## Description

Part of ENG-000

### Dependencies
None

### Description
Remove early return if roster is empty

### Testing
- Local
  - [x] run roster generation and make sure its not broken :)
- Staging
  - [ ] Run roster generation on an hie with no subscribers and see if error pops up.
  - [ ] Run roster generation on an hie with subscribers (no error should pop up).


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Roster generation now continues through downstream steps for zero-patient cases instead of exiting early.
  * Prevented unnecessary organization lookups when there are no identifiers, avoiding redundant external calls.

* **Changes**
  * Scrambled IDs are now converted to the Bamboo-specific format for Bamboo HIEs.
  * Logging narrowed to reduce noisy/preliminary warnings.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cffa1781607f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.