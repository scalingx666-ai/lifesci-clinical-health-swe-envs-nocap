# Issue

**Title:** [FIX] Match dynamic pack output path

## Description

In the deploy script, set pack dynamic output path to match static pack output path. This is currently different, causing release action not finding the resulting dynamic zipped pack.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27dfb1777594`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.