# Issue

**Title:** ENG-000 Revert Safer deploy to prod CICD

## Description

### Dependencies

- Upstream: 
- Downstream: none

### Description

Reverts 

This reverts commit 2c93ea18b2787bd3160c221b998ade140d8b940a, reversing
changes made to 29f63dcc3efc7913d3f0682a8038171b7907cf65.

### Testing

none

### Metrics

none

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Chores
* Simplified production and staging deployment workflows by removing manual branch validation gates and unnecessary job dependencies, enabling more streamlined and efficient deployment processes.
* Expanded automated deployment trigger logic by including additional service paths in change detection, ensuring deployments are triggered appropriately for a comprehensive set of code modifications across services.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56fa446975c5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.