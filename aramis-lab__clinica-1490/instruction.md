# Issue

**Title:** [REF] Search for SPM standalone execution file with pattern instead of hardcoding for spm12

## Description

Adresses part of #1481 regarding `_get_platform_dependant_matlab_command_for_spm_standalone`.


Rq : not sure it will do well with CI set-up

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `25e79021e0e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.