# Issue

**Title:** ENG-1230 Recreate HIE Directory entry view

## Description

### Dependencies

- Upstream: 

### Description

- Migration to create the combined HIE directory view
- Sending as a separate PR to avoid errors during deployment. Though, i'm now thinking it would've been safe to do on the same PR anyway

### Testing

- Local
  - [x]  apply the migration
  - [x] confirm the hie directory view contains orgs from both directories
- Staging
  - [ ] confirm the hie directory view contains orgs from both directories
- Production
  - [ ] confirm the hie directory view contains orgs from both directories

### Release Plan

- :warning: This contains a DB migration
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- New Features
  - Added endpoint to fetch CommonWell directory entries with optional filters and counts.
  - Added internal endpoints to rebuild CommonWell and Carequality directories.
  - Introduced a unified HIE directory view that merges and de-duplicates entries across networks.

- Improvements
  - More resilient, batched directory rebuilds with throttling and enhanced error reporting.
  - Separate delegate caches per network for safer, clearer authorization behavior.

- Chores
  - New configuration option for scheduling the CommonWell directory rebuilder.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41fc6c7e3c48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.