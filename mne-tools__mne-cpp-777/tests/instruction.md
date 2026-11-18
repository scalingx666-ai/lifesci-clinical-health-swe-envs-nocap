# Issue

**Title:** [MAINT,FIX] MNE Scan - plugin maintenance

## Description

- update signal slot syntax and class names in ftbuffer
- change plugin name for Filter plugin (formerly noise)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6458838e87e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.