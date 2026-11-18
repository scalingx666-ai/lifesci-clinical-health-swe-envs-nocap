# Issue

**Title:** [REF] Remove MATLAB + SPM set-up totally

## Description

Following the work on #1626, #1609, #1547, #1542 we can finally remove the whole SPM+MATLAB machinery from the code.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1464bf06a02f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.