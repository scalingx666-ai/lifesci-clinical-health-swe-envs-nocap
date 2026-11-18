# Issue

**Title:** feat(server): log when single-resource lookups match multiple resources

## Description

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Bot requests now use the bot’s project membership when available, with a fallback to the current user’s membership when it isn’t.
  * Searches for bots, agents, devices, and custom operations now handle matching records more consistently. When multiple records match, the server selects one and logs a warning.
* **Reliability**
  * Repeated warnings about the same issue are limited over time, helping keep server logs clearer. The warning limit resets after a set interval, so recurring issues can still be reported.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa6d79815db4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.