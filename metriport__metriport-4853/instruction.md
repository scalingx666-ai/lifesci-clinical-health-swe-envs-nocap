# Issue

**Title:** feat(fhir-sdk): if dates are out of order, flip them when trying to index in fhir-sdk

## Description

metriport/metriport-internal#1040

Ref: ENG-1242


### Dependencies

None

### Description

If dates are out of order during fhir sdk interval tree indexing, just swap them instead of failing.

### Testing

Already released + working in prod

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Improves stability when processing malformed date ranges (e.g., reversed bounds), handling them gracefully instead of failing. This reduces unexpected errors during indexing operations and increases resilience when working with imperfect data.

* **Chores**
  * Bumped fhir-sdk package version to 1.3.5.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55b1c146bcf7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.