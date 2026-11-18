# Issue

**Title:** fix(server): Resolve PlanDefinition action canonicals one resource type at a time

## Description

`readCanonical` in `PlanDefinition/$apply` now searches ActivityDefinition, then PlanDefinition, then Questionnaire, instead of searching all three types together. The existing version rule (most recently updated `active` first) applies only within the first type that has a match.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `92c8ce1381ea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.