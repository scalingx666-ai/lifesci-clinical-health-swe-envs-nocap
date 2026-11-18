# Issue

**Title:** Update preprocessing viz to address #318 and #296

## Description

A fair bit of refactoring, addition of the average heart rate per chunk being displayed, and updated documentation. This should be a fair bit more robust (tested on my laptop and my personal desktop, with somewhat different environments for VSCode and Jupyter Lab).

This should address #318 in particular, as well as #296 and related issues.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbf04579d944`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.