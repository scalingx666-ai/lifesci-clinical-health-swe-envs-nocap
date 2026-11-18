# Issue

**Title:** [MAINT] Clear measurement info when stopping hpi plugin

## Description

- Cleared saved Fiff Info and Digitizer Data when resetting plugin state.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea7593f0e159`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.