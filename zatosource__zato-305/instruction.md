# Issue

**Title:** GH #296 Quickstart error when using sqlite. Using an absolute path fixes...

## Description

Apparently, Django has some problems handling relative paths in this scenario, so converting it to a full one solves the problem.
However, I've seen that all of the configuration paths that I have seen are relative, so if you feel that this breaks the standard and that we'd better look for another solution please feel free to reject this one.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d66ac6bd407c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.