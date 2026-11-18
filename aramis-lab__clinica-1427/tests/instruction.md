# Issue

**Title:** [CI] Stop the macOS pipelines

## Description

Since the MacOS self-hosted runner is not working properly as a service, let's comment the related pipelines and avoid the consistently broken CI.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a8c4560ee3d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.