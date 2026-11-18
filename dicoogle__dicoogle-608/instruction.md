# Issue

**Title:** Update npm dependencies

## Description

Just a regular maintenance update to the npm packages.

- bump package locks via `npm update`, should invalidate most dependabot PRs
- update ESLint  to version 8
- ensure that `dicoogle-client` is in the latest version
   - v5.2.3 fixes known problems to the library

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dc1ba37dc979`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.