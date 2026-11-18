# Issue

**Title:** Ggraham 20260825 oracle codesystem

## Description

- use a semijoin instead of a distinct to avoid oracle clob comparison problem
- test 
- changelog

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49064b329945`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.