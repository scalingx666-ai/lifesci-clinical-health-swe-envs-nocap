# Issue

**Title:** [MAINT] Add rule for ignoring qt-creator generated build folders

## Description

Add entry to .gitignore so that QtCreator created build folders are ignored by git.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b33fd80a55e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.