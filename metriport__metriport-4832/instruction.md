# Issue

**Title:** ENG-554 Removing old internal patient commands

## Description

Part of ENG-554

### Description
- Removing deprecated routes 

### Testing
- N/A

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- Chores
  - Removed legacy CommonWell v1 admin tools: patient duplicate detection, duplicate resolution, and patient recreation at HIEs.
- Refactor
  - Eliminated related internal API endpoints for listing/patching duplicates and recreating patients, simplifying the medical patient routes.
- Documentation
  - Update any operational runbooks and admin references to reflect the removal of duplicate-handling and recreation workflows.
- Note
  - Admin users should transition away from the removed workflows; no alternative endpoints are provided in this release.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8c2840d58872`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.