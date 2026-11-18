# Issue

**Title:** RELEASE Update analytics script

## Description

Issues:

- https://linear.app/metriport/issue/ENG-000

### Dependencies

none

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
  - Adds a heads-up that lists patients without consolidated data when running with the --check-consolidated option.
  - Updates the confirmation step to include this information, providing clearer context before proceeding.
  - Displays a concise message when all patients have consolidated data, reducing uncertainty.
  - Ensures the new information is available before prompting, improving the flow of confirmations.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d8d2f522790`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.