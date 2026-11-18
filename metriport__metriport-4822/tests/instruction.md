# Issue

**Title:** ENG-1214 Remove CW DoA FF

## Description

Part of ENG-1214

### Description

- CW DoA flow works, so we don't need the FF anymore 

### Testing
- N/A

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- New Features
  - CommonWell (HIE) initialization is now always enabled for all users, providing consistent access without reliance on a feature flag. This should improve reliability and reduce intermittent availability issues.

- Chores
  - Removed the legacy feature flag and related configuration for CommonWell DOA, simplifying rollout and maintenance.
  - Cleaned up schema and datastore entries associated with the removed flag to prevent stale configuration.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2dfc7c26c13a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.