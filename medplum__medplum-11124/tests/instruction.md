# Issue

**Title:** Optimized Repository.searchResources

## Description

Avoid calculating links and round trips to the DB for total counts.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Search operations can request resource-only results. These responses include bundle entries, while metadata such as pagination links and totals may be omitted.
* **Bug Fixes**
  * Single-result searches now respect the configured minimum query limit when one is set.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `68c347e745a2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.