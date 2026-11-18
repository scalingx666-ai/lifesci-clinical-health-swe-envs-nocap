# Issue

**Title:** [FIX] Genfi-to-BIDS : modification of the source path of the image in scans tsv files

## Description

I will do the modification of the CI right after this one is merged and I rebased my branch for my other PR #1468. The nonregression tests should fail only because the scans files are now named `scans` and not `scan` in the CI reference.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4247631b0b01`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.