# Issue

**Title:** [FIX] PET-Volume : computes statistics with the 4 atlases again (not only 1)

## Description

The `break` was simply removed. Non-regression tests for PET-Volume happen weekly and not on PR updating so outputs were tested locally. Also, the non-regression tests for PET-Volume do not include the files of interest (atlas statistics) anyway so they were never tested. Now at least the pipeline use 4 atlases as it is supposed to. 

The PR also includes a new unit test for the function and renaming the test files accordingly.

Adding more complete non-regression tests for PET-Volume should be done, but in another PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d8ae5e2acfc9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.