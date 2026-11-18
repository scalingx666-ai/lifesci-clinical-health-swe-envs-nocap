# Issue

**Title:** [CI] Allow manual execution of anat test workflow

## Description

Revert modification of cron for anat testing workflows made in #1486 and use manual dispatch instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e42d198eb5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.