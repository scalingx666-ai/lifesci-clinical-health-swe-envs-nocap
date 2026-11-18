# Issue

**Title:** FIX: MNE Scan: use correct directory for hpi presets

## Description

- load preset relative to directory of the executable rather than current working dir.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `04e3c6c9d23d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.