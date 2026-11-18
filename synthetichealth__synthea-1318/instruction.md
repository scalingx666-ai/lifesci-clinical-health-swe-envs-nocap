# Issue

**Title:** Fix SDOH address category.

## Description

Fixes the PRAPARE SDOH module so that the "Address" observation has a category of `survey` instead of `laboratory`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `188ce6373ef9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.