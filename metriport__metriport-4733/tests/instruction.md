# Issue

**Title:** RELEASE Bamboo specific identifier scramble/unscramble + Konza timezone

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1081
- https://linear.app/metriport/issue/ENG-1122

### Dependencies
None

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

- New Features
  - Added Konza timezone detection for HL7 notifications.
  - Translate Bamboo-formatted patient IDs on receipt for improved interoperability.
  - Roster generation now formats patient IDs for Bamboo.

- Refactor
  - Cleaned up imports and streamlined HL7-related error handling.

- Tests
  - Roster generator tests updated to use a seeded ID-scrambling approach.

- Chores
  - Simplified sample HL7 sender script and noted Bamboo-specific segment usage.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `480ac579bc6d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.