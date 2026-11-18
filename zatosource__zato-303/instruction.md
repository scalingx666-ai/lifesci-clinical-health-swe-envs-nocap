# Issue

**Title:** Csala f gh264 add timeout to service invoke

## Description

Implemented live test cases as we discussed.
I took advantage of the chance to move all the logic for live testing into `code/zato-server/test/zato/server/live/__init__.py`, so now extending from class LiveTestCase is enough to cover the optional service deployment during tests.
I also increase the delay between service deployment and test execution to 1 second because in some cases the 200ms previously defined were not enough and the tests failed randomly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd82c9b61a0b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.