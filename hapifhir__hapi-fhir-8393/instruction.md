# Issue

**Title:** Fixing 8308 changelog type

## Description

- fixed value of changelog type to "perf"
- added changelog type constants
- added assertion in existing changelog test that validates the changelog type value
- updated migration unit test to use changelog type constants

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `03e6aa2f7934`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.