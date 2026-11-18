# Issue

**Title:** Build webapp on Maven execution

## Description

With the current setup, `npm install` does not build the webapp automatically.

- Add npm run build execution step to frontend-maven-plugin
- Update frontend-maven-plugin to latest version
- Update Node.js and npm to latest LTS

Should hopefully resolve some of the recent issues encountered while building Dicoogle 3.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0fe549ece131`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.