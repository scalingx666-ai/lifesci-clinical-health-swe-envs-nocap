# Issue

**Title:** First round of optimizing dispatch job

## Description

Various fixes to avoid lots of throwaway work and undesired cache-writes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24cad1ec492a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.