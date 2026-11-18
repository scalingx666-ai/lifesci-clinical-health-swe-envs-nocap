# Issue

**Title:** Update CI workflows to check Java and webapp separately

## Description

- add node.yml
   - build webapp using multiple versions of Node.js
- update maven.yml
   - build Java project using JDK 8 and 11
   - skip webapp
- update readme
   - some things do not have to be installed in the system

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `668a32d2a608`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.