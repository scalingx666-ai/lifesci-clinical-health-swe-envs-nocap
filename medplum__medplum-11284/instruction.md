# Issue

**Title:** Test parts of `@medplum/core` in both browser and NodeJs environments

## Description

This stemmed from working on expanding the capabilities of `packages/e2e` and seeing that `arrayBufferToBase64` in `packages/core/src/utils.ts` was not NodeJS-compatible.

Adds a second vitest project with `environment: 'node'` in packages/core/vite.config.ts

It'd be a good goal to get the entire `@medplum/core` test suite running in both environments with minimal `test.runIf()` in the name of stability; this is a good step in that direction.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b9894dda5986`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.