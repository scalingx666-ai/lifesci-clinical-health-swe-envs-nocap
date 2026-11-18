# Issue

**Title:** Loading FIFF would crash with empty raw-data directory

## Description

Loading FIFF would crash with empty raw-data directory. Make sure it gracefully fails and that any indices being accessed are valid.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55e5a59a3ef7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.