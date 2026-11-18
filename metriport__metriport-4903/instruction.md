# Issue

**Title:** feat(ehr): hcc condition fitlering + enabling elation

## Description

Ref: ENG-1303

### Description

- adding hcc filtering for conditions
- turning on elation

### Testing

- Local
  - [ ] skipped
- Staging
  - [x] test run elation patient
- Sandbox
  - [ ] N/A
- Production
  - [ ] turn on elation writeback for CX

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added HCC-based filtering for conditions during write-back operations, allowing users to filter by all conditions, HCC-only, or non-HCC-only.
  * Enabled write-back support for additional EHR sources beyond the previously supported system.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65332ad6e113`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.