# Issue

**Title:** [ENH] Create default FiffInfo for FtBuffer with minimal metadata

## Description

- Change logic to no longer expect (or need) neuromag extended header. Instead, default to minimal FiffInfo with made with data from simple ftbuffer header.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9953d7fc06ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.