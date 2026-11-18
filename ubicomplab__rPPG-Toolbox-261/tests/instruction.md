# Issue

**Title:** Fix typo in PhysFormer infer configs

## Description

This is a simple fix to modify the config's model name entry from "Tscan" to "PhysFormer" for all of the infer configs related to the PhysFormer model.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e33a44b3904`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.