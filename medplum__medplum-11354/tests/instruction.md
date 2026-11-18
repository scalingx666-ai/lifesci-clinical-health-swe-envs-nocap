# Issue

**Title:** Skip system-authored resources for Bot.runAsuser subscriptions

## Description

Previously, system-authored resources hit an error when attempting to execute a Bot with `runAsUser: true` via a subscription. This PRs formalizes that behavior.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21989eec1fb5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.