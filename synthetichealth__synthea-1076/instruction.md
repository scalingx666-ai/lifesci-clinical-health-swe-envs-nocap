# Issue

**Title:** Change beneficiary file export

## Description

Instead of three files (INSERTS, intermediary UPDATES, final UPDATES) now output one beneficiary file per year of export.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d90b4e3b1c41`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.