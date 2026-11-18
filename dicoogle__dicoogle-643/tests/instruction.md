# Issue

**Title:** Update logging dependencies and add jul-to-slf4j

## Description

### Summary

- Update logging dependencies:
   - slf4j to 1.7.36
   - log4j to 2.20.0
- Add `jul-to-slf4j` so that it is possible to collect logs from libraries using java util logging

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f18b919f81ac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.