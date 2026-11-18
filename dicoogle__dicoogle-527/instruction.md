# Issue

**Title:** Stop logging DICOM requests for C-FIND and C-MOVE SCP - v2

## Description

Stop using LogDICOM in v2.
All discussion about v3 and stop using or refactor LogDICOM is out of the scope here.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `385c53f85b86`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.