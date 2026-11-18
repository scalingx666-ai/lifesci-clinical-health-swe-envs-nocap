# Issue

**Title:** ci: disable coverage checking action for now

## Description

It has a permission issue with PRs from forks, and until we figure out how to fix that securely, let's just disable the check.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `067997e8b04b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.