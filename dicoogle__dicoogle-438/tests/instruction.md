# Issue

**Title:** Update my email address in package manifests

## Description

Only in the package.json files. It would be pointless to edit all those @author directives.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `210853d7f207`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.