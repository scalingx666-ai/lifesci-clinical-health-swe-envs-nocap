# Issue

**Title:** [ENH,MAINT] WASM script

## Description

- Added was script for downloading and building dependencies and the project.
- Used script in GitHub Actions.
- Changed GitHub Actions to use newer versions of emsdk (3.1.20) and qt (5.15.5)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e40b689d343d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.