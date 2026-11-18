# Issue

**Title:** Fixed the bugs for TS-CAN

## Description

Negative pearson does not work for TS-CAN. Need to look into further. Switched to MSE for now. 

@Xiaoyu-SZ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c63e7c0d795d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.