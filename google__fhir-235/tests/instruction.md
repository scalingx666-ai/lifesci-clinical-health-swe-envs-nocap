# Issue

**Title:** Fixes bug in ProtoFilePrinter where fields with no oneof were treated as part of the zeroth oneof if it exists, and field descriptions were dropped.

## Description

Fixes bug in ProtoFilePrinter where fields with no oneof were treated as part of the zeroth oneof if it exists, and field descriptions were dropped.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2b874ae0b73`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.