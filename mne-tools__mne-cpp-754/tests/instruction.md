# Issue

**Title:** [FIX] MNE Analyze leak fix, library get function fix

## Description

- fix leak in communicator pointer not being deleted (used shared pointer)
- fix clearing of averaging views by returning correct pointer when getting evoked set and evoked model

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4b4c7219873`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.