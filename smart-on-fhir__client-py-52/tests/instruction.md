# Issue

**Title:** Add include method to FHIRSearch objects

## Description

This adds the ability to use `_include` and `_revinclude` with FHIRSearch objects (#13). It supports only simple forward or reverse includes - no recursive or iterative includes.

Also fixes a small typo in FHIRSearch (#35)!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4455e0b0001d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.