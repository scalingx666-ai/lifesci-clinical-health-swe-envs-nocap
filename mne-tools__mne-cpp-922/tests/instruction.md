# Issue

**Title:** [MAINT] Update Github Actions Runners

## Description

Ubunutu 18.04 is currently [deprecated and will soon be axed completely](https://github.blog/changelog/2022-08-09-github-actions-the-ubuntu-18-04-actions-runner-image-is-being-deprecated-and-will-be-removed-by-12-1-22/)

This PR changes actions to use `ubuntu-20.04` wherever a "minimum" version is appropriate, or `ubuntu-latest` elsewhere.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac3a7170c41b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.