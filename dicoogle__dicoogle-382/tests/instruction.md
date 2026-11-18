# Issue

**Title:** Update frontent development component versions: Node.js 10 + npm 6

## Description

- update frontend-maven-plugin to 1.7.5
- update Node.js minimum version to 6, recommend latest LTS or Stable
- make frontend plugin install Node.js 10.15.3 and npm 6.4.1
- update npm minimum to v4, recommend v6
- document changes in the README files

This is also an attempt to fix #381, as the latest version of the frontend plugin is more likely to have fixed this one.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0dc6675e5618`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.