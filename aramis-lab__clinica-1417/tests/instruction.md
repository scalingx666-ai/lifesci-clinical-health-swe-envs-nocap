# Issue

**Title:** [MAINT] Bump poetry to v2

## Description

Remove temporary fix made in #1410 and bump poetry to v2.

Poetry was updated to v2.0.1 on the CI machines.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cdafc27ba96c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.