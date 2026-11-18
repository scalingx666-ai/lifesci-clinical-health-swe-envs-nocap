# Issue

**Title:** Remove JSON name for the reference.uri field as it was causing a collision with the 4.* version of the protobuf Python library.

## Description

Remove JSON name for the reference.uri field as it was causing a collision with the 4.* version of the protobuf Python library.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f32916bea2d1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.