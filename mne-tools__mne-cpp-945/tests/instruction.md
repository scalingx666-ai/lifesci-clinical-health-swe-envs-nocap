# Issue

**Title:** [MAINT, FIX] Update Coverity Scan

## Description

Change build command in an attempt to fix coverity scan. Also update qt version in the meantime.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `666eb9b1f33f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.