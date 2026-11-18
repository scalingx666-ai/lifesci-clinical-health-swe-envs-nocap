# Issue

**Title:** Require Bot.runAsUser or `ProjectMembership`, strict `searchUnique`

## Description

This is a followup to

Searches for bots, agents, devices, and custom operations now must match exactly one resource. If multiple resources match, a 412 error is thrown.

Bots must now either have `Bot.runAsUser` set to `true` or it must have a `ProjectMembership`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b335ae63a7ce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.