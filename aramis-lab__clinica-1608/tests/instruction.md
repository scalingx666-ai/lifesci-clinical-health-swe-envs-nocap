# Issue

**Title:** [FIX] Fix command setting with MAC for SPM

## Description

How to test : SPM25 standalone + MCR set-up with pipelines T1-Volume / PET-Volume

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6e6fcd258d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.