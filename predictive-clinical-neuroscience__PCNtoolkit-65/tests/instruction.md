# Issue

**Title:** Add transfer function BLR

## Description

I think how I adjusted the mean 'line 418' for all the covariates is not correct when there is a difference in covariates used between the original site and the transfer site.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1ada01160e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.