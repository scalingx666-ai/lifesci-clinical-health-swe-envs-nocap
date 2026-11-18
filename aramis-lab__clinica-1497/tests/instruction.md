# Issue

**Title:** [FIX] Fix imports in `pet-surface`

## Description

After creation of `pipelines.pet` module some functions were moved to `pet.utils` from `utils.pet` but imports were not changed for `pet-surface`. This pipeline is also expected to be in this module (cf #1237) but in the meantime these imports should be fixed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b04bcd8d88d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.