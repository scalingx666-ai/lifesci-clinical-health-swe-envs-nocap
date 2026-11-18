# Issue

**Title:** TRUNK-6756: Remove deprecated Daemon thread-execution overloads

## Description

TRUNK-6756: Remove deprecated Daemon thread-execution overloads

## Description of what I changed

Removed the deprecated Daemon thread-execution overloads and the tests that specifically covered those removed overloads.

## Issue I worked on

see https://issues.openmrs.org/browse/TRUNK-6756

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project.

- [ ] I have **added tests** to cover my changes. (If you refactored existing code that was well tested you do not have to add tests)

- [x] I ran `./mvnw clean package` right before creating this pull request and added all formatting changes to my commit.

- [x] All new and existing **tests passed**.

- [x] My pull request is **based on the latest changes** of the master branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `51e78cea7d06`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.