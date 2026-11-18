# Issue

**Title:** [REF][TEST] OASIS3-TO-BIDS : improve code quality

## Description

Done : 
- Code refactoringto remove less useful parts 
- Add unit tests

RQ : PET metadata not used ?
_Reminder_ to change CI data at the end of the refactoring
@davidaquilue if you want to check it out

New issue to write : add more metadata to OASIS3 files ?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4550ed57dd30`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.