# Issue

**Title:** Permit bind *:11223 in haproxy

## Description

The original pyparser configuration allowed IP or hostname only.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe8684eae5d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.