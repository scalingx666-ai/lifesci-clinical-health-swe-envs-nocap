# Issue

**Title:** Develop 2.7.4

## Description

Features:

 - Lasso regression instead of Ridge
 - Calibration for v2 is not changing its acceptance radius anymore while running

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4e7b7a0e8d5a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.