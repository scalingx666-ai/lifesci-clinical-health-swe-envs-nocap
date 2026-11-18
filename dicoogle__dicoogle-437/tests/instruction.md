# Issue

**Title:** Do not require Node.js 15 and npm 7 to pass in CI

## Description

Should make our CI pass again.

My concern here is that Node.js 15 also introduces npm 7, a version which also introduces a few changes in behavior, as well as in the package lock format. As such, I propose we not guarantee these version to work for now, while recommending to always stick to the latest LTS, to be reiterated on a later stage.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8c5a86aa9612`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.