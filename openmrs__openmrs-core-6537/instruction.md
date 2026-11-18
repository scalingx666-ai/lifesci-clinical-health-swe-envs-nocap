# Issue

**Title:** TRUNK-6796: Fix NPE whe death date is null when merging patients

## Description

## Changes
Fixes the incorrect null check for priorDateOfDeath.
Adds a test to make sure computeHashValue() does not throw an exception when priorDateOfDeath is null.

## Issue I worked on
See : https://openmrs.atlassian.net/browse/TRUNK-6796

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the **code style** of this project.
- [x] I have added tests to cover my changes. *(These are minor code quality fixes that do not require new tests.)*
- [x] I ran `./mvnw clean package` right before creating this pull request and added all formatting changes to my commit.
- [x] **All new and existing tests passed.**
- [x] My pull request is **based on the latest changes of the master branch.**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `015b9c67043f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.