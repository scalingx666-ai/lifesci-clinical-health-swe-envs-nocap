# Issue

**Title:** OBPIH-8064 part 2: make Sentry work for GSPs

## Description

Part 2 of  Makes sentry work with GSPs. I moved this to its own PR for easier review.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `50a735afcc24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.