# Issue

**Title:** Webapp maintenance (2024)

## Description

### Summary

- dependency: ~~react-router 4~~
   - Reverted, to be tried again at a later date.
- dev-dependency: css-loader 7
- dev-dependency: sass-loader 14
- dev-dependency: style-loader 4
- dev-dependency: webpack-dev-server 5
- dev-dependency: eslint 9
- `npm update` so that other dependencies are refreshed
- `npm update` on webcore
- Require a minimum of Node.js 18 to build the webapp

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15c65f503932`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.