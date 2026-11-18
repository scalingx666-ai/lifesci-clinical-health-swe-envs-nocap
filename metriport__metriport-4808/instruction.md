# Issue

**Title:** RELEASE Eng-1201 queue appointment WH linking

## Description

Issues:

- https://linear.app/metriport/issue/ENG-1201

### Description

- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- New Features
  - Streamlined patient linking during appointment webhooks for Elation and Healthie, improving match accuracy.
  - Automatic data quality checks triggered during patient sync for more reliable records.
- Bug Fixes
  - The setting to disable appointment patient processing is now consistently honored.
- Refactor
  - Unified identifier naming (practiceId/patientId) across EHR flows for consistency.
  - Standardized link-and-sync workflow to improve reliability and maintainability without changing overall behavior.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9057c34da1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.