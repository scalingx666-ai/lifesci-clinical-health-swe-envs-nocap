# Issue

**Title:** [MAINT] Fix Windows Plugin Deployment and Fix TMSI Plugin Build Issues

## Description

- Fix deployment location of win plugins.
- Fix issues in TMSI plugin that were preventing it from building.
- Add `tmsi` option to build script on windows.
- Update documentation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ccb2a89f70a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.