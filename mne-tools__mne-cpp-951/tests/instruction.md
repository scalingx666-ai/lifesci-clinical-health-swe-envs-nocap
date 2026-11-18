# Issue

**Title:** [MAINT] Coverity Static Analysis

## Description

- Move shell script portion of CI to its own script.
- Make further changes to script logic to accommodate cmake and running locally.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c438e418fbbc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.