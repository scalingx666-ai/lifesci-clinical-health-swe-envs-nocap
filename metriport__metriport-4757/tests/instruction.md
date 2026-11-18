# Issue

**Title:** RELEASE Update XCPD lambda to init FFs

## Description

Issues:

- https://linear.app/metriport/issue/ENG-000

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

- **New Features**
  - Introduced feature flag support in the IHE Gateway V2 for controlled rollouts.
  - Outbound patient discovery now initializes feature flags at startup.

- **Chores**
  - Infrastructure updated to share the feature flags data source across stacks for consistent access.

- **Refactor**
  - Minor import/organization cleanup with no user-visible behavior changes.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `33ed9800af0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.