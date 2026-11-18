# Issue

**Title:** Graphviz updates

## Description

This should wait until #1144 is merged.

Updates the version of the graphviz library used by Synthea and makes code changes to deal with the new API.

This also cleans up some oddness discovered in HIV submodules related to date comparisons.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d90e086985a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.