# Issue

**Title:** Progress codespell forward, fixup typos it detects

## Description

Is there a CI run to run codespell or pre-commit?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9e00123c373`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.