# Issue

**Title:** Use US Core 6 as default in properties file

## Description

The code was updated to use US Core 6 as the default when no US Core version is set (), but `synthea.properties` was still set to default to US Core 5.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a65f56f13e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.