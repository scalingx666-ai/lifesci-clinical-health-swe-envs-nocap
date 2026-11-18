# Issue

**Title:** [C-MOVE] Fix problem related with infinite loop if skip IS returns 0

## Description

Fix problem related with infinite loop if the `skip` method of` InputStream` implementation does not do the job and returns 0.
This can happen with `CipherInputStream` with  `BuferedInputStream` wrapper.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01310a7e3905`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.