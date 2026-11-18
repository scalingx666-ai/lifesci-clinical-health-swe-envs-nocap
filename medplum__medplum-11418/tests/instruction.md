# Issue

**Title:** fix(server): omit Binary.data from subscription notifications

## Description

Rest-hook, Bot and WebSocket subscription notifications for a Binary with inline `data` now omit `data` and tag the resource as SUBSETTED; subscribers read the content from binary storage. The stored resource is unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a91cce07380`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.