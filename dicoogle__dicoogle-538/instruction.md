# Issue

**Title:** Check whether confs dir exists before creating it in ServerSettingsManager

## Description

May seem redundant, but this check prevents the program from trying to create a directory if a symlink directory already exists.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `582f9f997736`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.