# Issue

**Title:** Fix cases where the Go jsonformat library would modify the input proto when marshalling to JSON

## Description

Fix cases where the Go jsonformat library would modify the input proto when marshalling to JSON

Also adds code to the tests to ensure that the input is not modified

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a330776e20e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.