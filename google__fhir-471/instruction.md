# Issue

**Title:** Fix disallowNull option to not error on false bools & ints of value 0, but still on empty strings.

## Description

Fix disallowNull option to not error on false bools & ints of value 0, but still on empty strings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd3e81c96136`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.