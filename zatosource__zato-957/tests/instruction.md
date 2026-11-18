# Issue

**Title:** Sap fixes

## Description

I ran into some problem with the SAP connector on the current support/3.0 branch. A missing decrypt_func that crashed zato when restarted after a config change. And a connection wrapper that needed to inherit from the base Wrapper.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8f1efde80db5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.