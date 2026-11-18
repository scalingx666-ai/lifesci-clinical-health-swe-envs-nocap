# Issue

**Title:** Handle non-ASCII chars in traceback

## Description

Avoid hiding original error and traceback with 'UnicodeDecodeError' when traceback contains non-ASCII characters.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60c7780004c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.