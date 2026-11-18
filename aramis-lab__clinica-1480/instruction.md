# Issue

**Title:** [FIX] Remove the `--yes` option from the `t1-volume` pipeline as it is not used anymore

## Description

Following #1419, this option should not be in the client for the pipeline anymore. The PR also modifies the documentation for SPM12 installation for more clarity.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `64dd0c670ca8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.