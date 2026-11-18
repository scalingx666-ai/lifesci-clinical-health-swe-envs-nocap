# Issue

**Title:** Dev

## Description

Changes:
- Update Dockerfile
- Add `scaler.transfer`, using Welford's algorithm to compute running mean and std for standardizers.
- Correctly save metadata of transfered models.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `89f44419cda3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.