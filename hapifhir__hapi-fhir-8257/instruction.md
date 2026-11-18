# Issue

**Title:** 8252 - Fix NPE that could occur in findContainedResource

## Description

Added two tests to catch Null Pointer Exception.
Added fix to findContainedResource to stop NPE.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d7494bf98fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.