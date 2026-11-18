# Issue

**Title:** Fixing the RMSE standard_error calculation in unsupervised_predictor.py

## Description

The square root was missing in standard_error calculation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc143fd53fad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.