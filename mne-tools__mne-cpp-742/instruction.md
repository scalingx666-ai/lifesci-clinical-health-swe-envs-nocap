# Issue

**Title:** [ENH,MAINT] Outsource test running from CI to scripts

## Description

This PR includes:

- Add scripts (/tools/testing) and outsource calling of tests from CI. This way devs can run tests locally more easily.
- Add corresponding documentation to contribution guide

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c03f79bc35d1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.