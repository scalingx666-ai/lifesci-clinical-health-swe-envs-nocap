# Issue

**Title:** fix: remove duplicate meta section from _Patient

## Description

The `_Patient.liquid` template includes two `meta` sections. This PR combines the two sections.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa11e12b7ab5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.