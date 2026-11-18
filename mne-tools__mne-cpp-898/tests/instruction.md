# Issue

**Title:** [MAINT] Update windows runner for min version

## Description

Due to the , all runs that used `windows-2016` have been made to use `windows-2019` instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38bc3ba5213b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.