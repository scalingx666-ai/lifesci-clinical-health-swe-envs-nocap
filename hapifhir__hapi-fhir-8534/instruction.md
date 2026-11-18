# Issue

**Title:** Extract error handling routine in RestfulServer.java

## Description

This allows externally handled errors (e.g. from Spring Security) to use the RestfulServer error handling.

Fixes:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd4b5fc2457b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.