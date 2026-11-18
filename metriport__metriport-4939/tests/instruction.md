# Issue

**Title:** feat(ihe): fix broken s3 path

## Description

Ref: ENG-1052

### Description

- s3 path was wrong

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Corrected cloud storage path construction for partitioned/parsing results so path segments are joined consistently and trailing separators are preserved, ensuring stored data is organized and addressed correctly.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c2033f4ff9b6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.