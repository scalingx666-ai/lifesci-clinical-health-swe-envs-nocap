# Issue

**Title:** fix(frontend): wait for the tab strip to mount before scrolling it in e2e tests

## Description

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Tests**
  * Expanded coverage for scrolling through overflowing tabs on connected user pages, including mouse-wheel, line-based wheel, and edge-arrow interactions. This helps verify that users can navigate the full tab strip when its contents extend beyond the visible area.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8dc855fe8c47`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.