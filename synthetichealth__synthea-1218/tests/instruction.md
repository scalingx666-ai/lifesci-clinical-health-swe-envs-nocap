# Issue

**Title:** Add exponential distribution for Length of Stay

## Description

This pull request adds the [exponential distribution](https://en.wikipedia.org/wiki/Exponential_distribution) [Wikipedia] to the list of available distributions.

This distribution can be used for determining "length of stay", for instance.

Addresses #1168 for the purposes of #1169, #1170, #1171

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47b822491f91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.