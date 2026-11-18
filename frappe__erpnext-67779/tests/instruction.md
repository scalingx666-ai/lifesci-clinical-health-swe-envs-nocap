# Issue

**Title:** chore: require frappe v16.60.0

## Description

**Problem**
ERPNext v16 needs Frappe v16.60.0 but still allows Frappe `>=16.55.0`.

**Fix**
Raise the minimum Frappe version to `16.60.0`.

**Steps to reproduce**
1. Set up a bench on Frappe v16.56.0.
2. Run `bench get-app erpnext --branch version-16-hotfix`.
3. Bench installs it without a version warning.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f86f1fb9d983`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.