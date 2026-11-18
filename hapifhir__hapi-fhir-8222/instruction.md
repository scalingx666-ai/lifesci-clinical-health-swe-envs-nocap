# Issue

**Title:** Make migrator check optional

## Description

#8028 introduced a new baseline capability. It looks like this is interfering with the way that Smile handles migrations, so this PR adds a new flag to explicitly enable the baseline check.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa9636bb08cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.