# Issue

**Title:** [ENH] Use more cpu

## Description

Hi, I've been trying to reduce compilation times. Noticed that with physical cores only ±50% of the cpu was used. Could you try this?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0d10f93c759`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.