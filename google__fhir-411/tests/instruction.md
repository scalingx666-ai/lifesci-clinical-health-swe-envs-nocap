# Issue

**Title:** Fix a bug in FHIRPath that caused children() to include the nodes in the input collection if they are primitive types.

## Description

Fix a bug in FHIRPath that caused children() to include the nodes in the input collection if they are primitive types.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `265b40f83f2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.