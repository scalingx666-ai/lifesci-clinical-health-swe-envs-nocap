# Issue

**Title:** RELEASE add alert to roster generation + add custom ai summaries

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-000

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

- Bug Fixes
  - Capture and report an error when a roster is empty to reduce silent failures.
  - Continue processing with empty patient sets instead of early-returning, improving end-to-end handling.

- New Features
  - Add two AI summary types (Cardiac Care and Nitrates & Conditions) with prompt templates and selection logic.
  - Expose feature-flag checks to enable these AI summaries per customer.

- Chores
  - Initialize telemetry earlier for consistent event recording.
  - Added guards to skip unnecessary external requests when inputs are empty and local config/flags initialization.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3cd44e48b6a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.