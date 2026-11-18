# Issue

**Title:** [FIX] Temporarily comment ADNI changes on dev for release

## Description

Related to PR #1617 and #1627 . Should be reverted for ADNI release

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73225f75a71f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.