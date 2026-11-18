# Issue

**Title:** Repair Django "AppRegistryNotReady: Apps aren't loaded yet." error

## Description

After upgrade from 2.0.7 to 2.0.8, Django Library upgraded from 1.3 to 1.7 so this caused issues with using Template.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea2e43606d81`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.