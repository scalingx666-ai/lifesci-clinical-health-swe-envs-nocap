# Issue

**Title:** Clean up logging around indexing tasks

## Description

### Summary

- lower level of some log lines which are not very useful (info to debug)
- remove commented out code

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `471e530aa5ba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.