# Issue

**Title:** MAINT: Fix filter plugin crash in MNE Scan, add min buffer read size.

## Description

- Prevent out of bounds access to Eigen structure that was sometimes causing a crash.
- Add min sample window to read from ftbuffer (quick fix for how filter plugin does max filter size).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ecb142b8899`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.