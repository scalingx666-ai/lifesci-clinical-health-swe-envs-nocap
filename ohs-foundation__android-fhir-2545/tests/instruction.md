# Issue

**Title:** Update CODEOWNERS to assign listed individuals instead of group as reviewers of PRs

## Description

This initial list matches https://github.com/orgs/google/teams/android-fhir-reviewers.

We were not able to get @google/android-fhir-reviewers working; see  for background, this PR is an alternative to that one.

See  for overall motivation.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `67c95299e3df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.