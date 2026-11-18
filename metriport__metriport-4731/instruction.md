# Issue

**Title:** RELEASE - update removal policy for mllp server ecr repo

## Description

### Dependencies

None

### Description

In order to help the Hl7 notification stack be able to boot up / down on its own without hacks, we need to change the removal policy on the ecr repo.



### Testing

Deployed fine to staging, and production diff looks safe - see feature pr.

Check each PR.

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- Refactor
  - Consolidated container image repository into a single, lifecycle-managed resource with automatic cleanup, improving consistency and reliability.
  - Streamlined infrastructure configuration and standardized dependencies; removed duplicate setup.
  - Preserves existing stack outputs and external behavior (no changes to integration points).

- Chores
  - Minor internal type/import adjustments to align with best practices.

No user-facing changes.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2db94cb39585`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.