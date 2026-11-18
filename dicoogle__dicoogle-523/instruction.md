# Issue

**Title:** Update important webapp dependencies

## Description

- Update `dicoogle-client` to `^5.1.0` (also in `webcore`)
   - 5.0.1 patches failures when trying to unindex or remove a large number of files (more info in bioinformatics-ua/dicoogle-client-js#28)
   - 5.1.0 adds `getPlugins`
- Update dev dependencies `@babel/core`, `@babel/preset-env`, `@babel/preset-react`
   - This in turn keeps `browserslist` updated for the best bundling results

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5507ee7d8b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.