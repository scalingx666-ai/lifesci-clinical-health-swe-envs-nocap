# Issue

**Title:** ENG-954 Temporarily remove analytics stack

## Description

### Dependencies

none

### Description

Temporarily remove analytics stack - context

### Testing

none

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- Chores
  - Disabled analytics platform integration, preventing analytics resources from being provisioned.
  - Analytics/telemetry events are no longer collected or forwarded from the API; related dashboards and reports may stop updating.
  - Historical analytics data remains available, but no new data will be recorded.
  - No changes to public APIs or application features beyond analytics collection behavior.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9ee98bd96df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.