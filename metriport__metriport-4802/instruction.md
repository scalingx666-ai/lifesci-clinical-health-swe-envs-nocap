# Issue

**Title:** RELEASE: Recent visit custom ai summary

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/CS-2472
- https://linear.app/metriport/issue/CS-2473

### Dependencies

- Upstream: none
- Downstream: none

### Description

- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this
- [ ] Update FF



<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Per-customer "recent visit" AI summary mode with dedicated prompts and date handling.
  * Adaptive timeframe selection for AI data preparation (tries 1 year, expands to 2 years and reports timeframe used).
  * Feature-flag helpers and a default flag to enable recent-visit mode for specific customers.
* **UI / Reports**
  * Conditions table adds a "Chronic" column and appends additional condition codes.
* **Bug Fixes**
  * Medication filtering fixed to include only active or unknown statuses.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ec8bdf797e4a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.