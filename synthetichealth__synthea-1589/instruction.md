# Issue

**Title:** Add labs/reports to clinical notes.

## Description

This is a minor change to add labs/reports to the clinical notes templates, and the removal of two unused imports.

The notes change is useful for downstream enhancements, for example, those provided by [synthetichealth/chatty-notes](https://github.com/synthetichealth/chatty-notes).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c807432af76a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.