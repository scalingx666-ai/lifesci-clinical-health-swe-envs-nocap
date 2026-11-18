# Issue

**Title:** Drop console calls in webapp js bundle

## Description

This used to be the case before the migration to Webpack, but they were brought back by mistake. Calls to `console.log` were only meant to be used in development mode.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2b48254b086`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.