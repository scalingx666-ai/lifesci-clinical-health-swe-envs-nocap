# Issue

**Title:** Unindex by DIM attribute

## Description

This is part one of an improvement to Dicoogle's unindexing capabilities (). Makes it so that this service endpoint can receive a list of instance, series or studies from the user, thus allowing for significantly smaller HTTP requests when unindexing a lot of data.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `434d25d7335a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.