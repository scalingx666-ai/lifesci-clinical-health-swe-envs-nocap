# Issue

**Title:** init.sh fails due to incorrect index

## Description

init.sh fails to run properly due to cmake_args index being incorrect. The CMAKE_PREFIX_PATH is actually index 6. Fixing it to not require an index at all.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f46d3b4149b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.