# Issue

**Title:** Reorder condition onset and diagnosing encounter in asthma module

## Description

Reorder two states in the branch where childhood asthma becomes lifelong asthma. Previously the diagnosing encounter preceded the condition onset, this PR switches the order so the onset is before the diagnosing encounter.

Fixes: #1655

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa0772fb5e92`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.