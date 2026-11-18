# Issue

**Title:** fix(ci): skip Docker Hub service credentials when secrets are unavailable

## Description

Fork PRs don't receive secrets, so the service container credentials evaluated to empty strings and failed workflow template validation. Set credentials to null when DOCKERHUB_USERNAME is missing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `549291c8df71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.