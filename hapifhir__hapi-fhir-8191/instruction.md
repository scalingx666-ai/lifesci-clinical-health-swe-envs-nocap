# Issue

**Title:** Add pointcut for modifying submitted batch2 jobs

## Description

A new pointcut has been added that can be used to modify requested batch2 jobs, overriding the job definition and/or parameters.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9953a7fdaf54`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.