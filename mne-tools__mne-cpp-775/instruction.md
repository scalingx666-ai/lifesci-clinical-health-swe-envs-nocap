# Issue

**Title:** [FIX] Fix MNE Scan crashing on stop

## Description

- In ScalingView destructor, remove map entry when deleting pointers to avoid infinite loop.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `84b607dd4436`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.