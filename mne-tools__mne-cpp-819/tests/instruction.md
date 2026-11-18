# Issue

**Title:** WIP [MAINT] Update CI linux runner version

## Description

- Update runners from 16.04 to 18.04. Unsure if minQt workflows running Qt 5.10 will like this.
- Might be a good time to discuss minimum requirements for compilers and OSs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b743770a0b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.