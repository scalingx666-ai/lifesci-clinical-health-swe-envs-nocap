# Issue

**Title:** ENG-954 re-add analytics stack

## Description

### Dependencies

- Upstream: 
- Downstream: none

### Description

Re-add analytics stack

This reverts commit d9e26dacb2074c3767dc70e95338934e5f0f0545, reversing changes made to d9ee98bd96df47af79fa0eee67439183f1bc9d29.

### Testing

- staging
   - [ ] analytics stack gets recreated

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Enabled the Analytics Platform in non-sandbox environments, making analytics capabilities available where applicable.

* **Chores**
  * Updated infrastructure logic to conditionally deploy the Analytics Platform only outside sandbox environments, preventing unnecessary stack creation during sandbox usage.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9e26dacb207`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.