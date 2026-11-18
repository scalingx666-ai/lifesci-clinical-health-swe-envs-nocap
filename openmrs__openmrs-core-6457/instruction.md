# Issue

**Title:** TRUNK-6758: Remove MigrationHelper

## Description

## Description of what I changed

Removed the deprecated `MigrationHelper` class from `org.openmrs.migration`. Since it was the only class in that package and had no remaining callers in core, the package is now removed as well.

## Issue I worked on

see https://issues.openmrs.org/browse/TRUNK-6758

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the code style of this project.

- [x] No new tests were needed because this change only removes deprecated, unused code.

- [x] I ran `./mvnw clean package` right before creating this pull request.

- [x] All new and existing tests passed.

- [x] My pull request is based on the latest changes of the master branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c1b124b30b5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.