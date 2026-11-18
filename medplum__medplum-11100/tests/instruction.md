# Issue

**Title:** chore(server): optimize Binary resources in expunge

## Description

Project expunges already delete all of a Project's Binaries by projectId, so they no longer also collect Binary IDs from attachment URLs. Compartment expunges only delete Binaries named in attachment URLs when they are in the same Project as the resource that names them.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15315988ca4a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.