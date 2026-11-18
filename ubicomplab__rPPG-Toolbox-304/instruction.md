# Issue

**Title:** Update SE calculation for RMSE to be more robust to large squared errors

## Description

As the title suggests, this makes the standard error calculation for RMSE more robust to large squared errors. This is done by scaling the the standard error relative to the RMSE, which is less sensitive to possible outliers.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `70eb133c4adb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.