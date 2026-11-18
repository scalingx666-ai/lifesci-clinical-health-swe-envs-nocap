# Issue

**Title:** Use default template provider if containerUrl is empty

## Description

Currently, if containerUrl is empty, the factory attempts to create blob template provider and throws on null containerUrl. 
Instead it will be better to use default template provider and not throw on initialization.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c231e9a7b5c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.