# Issue

**Title:** :bug:(fix) issue due to extention method

## Description

Lower dart version causing the below error
>This requires the 'extension-methods' experiment to be enabled.
>Try enabling this experiment by adding it to the command line when compiling and running.

By updating dart sdk issue is resolved.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `862db9e90074`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.