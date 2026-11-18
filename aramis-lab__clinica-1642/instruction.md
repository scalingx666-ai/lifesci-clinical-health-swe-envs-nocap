# Issue

**Title:** [TEST] Only use `clinica.all` module in workflows

## Description

Now that the set-up with MATLAB + SPM has totally been removed from the code of clinica #1624 there is no reason to keep a module for `clinica` (previously with this outdated set-up) and one for `clinica_standalone`. There is now only one module `clinica` on CI machines which loads the standalone set-up. This PR includes the modifications to use it on every relevant workflow.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a99b04ad3af2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.