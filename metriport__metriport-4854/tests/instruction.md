# Issue

**Title:** feat(ehr): procedure filtering

## Description

Ref: ENG-1221

### Description

- filtering procedures by CPT code

### Testing

- Local
  - [x] CPT codes in the array are written
- Staging
  - [x] CPT codes in the array are written
- Sandbox
  - [ ] N/A
- Production
  - [ ] CPT codes in the array are written

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added ability to restrict EHR write-back of Procedure records by CPT code.
  * Write-back filters now support an optional list of allowed CPT codes; Procedures lacking a matching CPT code are skipped.
  * Improves control over synchronization, reducing unintended or irrelevant Procedure write-backs and making results more predictable for users and administrators.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60dbdc5528f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.