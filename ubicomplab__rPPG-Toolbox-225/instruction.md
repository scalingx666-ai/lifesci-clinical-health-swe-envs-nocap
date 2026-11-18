# Issue

**Title:** Remove extra - 1 from diffnormalized len

## Description

Fix based on a small bug called out in #224. I just removed the extra `- 1` term.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d992de556fbb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.