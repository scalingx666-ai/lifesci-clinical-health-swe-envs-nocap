# Issue

**Title:** [MAINT] Stability improvements to stopping measurements in FtBuffer and MNE Scan

## Description

- Add outs for loops where fetching data could get stuck.
- Change order of function calls when ending measurements.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b3dbf8f293b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.