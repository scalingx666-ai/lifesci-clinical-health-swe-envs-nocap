# Issue

**Title:** Bug fix: transfer.get_mcmc_quantiles

## Description

- adds if-else statement to get_mcmc_quantiles 
- specifies predict_on_new_sites to sample full range of parameters

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `305c7ffd3363`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.