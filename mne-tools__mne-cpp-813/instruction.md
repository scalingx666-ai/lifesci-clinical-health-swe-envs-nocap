# Issue

**Title:** [WIP] MAINT, FIX: Change FtBuffer stop to fix crash and add thread interupt request before stopping plugins

## Description

- Remove internal requestInterruption/wait in ftbuffer stop function
- Add requestInterruption to all plugins before calling stop.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15a312113771`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.