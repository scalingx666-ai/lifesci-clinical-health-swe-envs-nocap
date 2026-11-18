# Issue

**Title:** Moves json_util to cc/json/ package.

## Description

Moves json_util to cc/json/ package.

This is a step in cleaning up the core cc/ package to remove non-top-level APIs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90496a90a727`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.