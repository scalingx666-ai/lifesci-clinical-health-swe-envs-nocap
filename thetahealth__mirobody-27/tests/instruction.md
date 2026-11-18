# Issue

**Title:** fix: make SQL logging optional in execute_query

## Description

## Summary
- add a `log_sql` flag to `execute_query`
- skip SQL statement logging when callers explicitly disable it
- preserve the existing logging behavior by default

## Verification
- python -m py_compile mirobody/utils/db.py

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9315046dc2c3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.