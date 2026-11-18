# Issue

**Title:** fix(server): retire outstanding password links on password change and rescope

## Description

When a user's password is set (by link, change password, or admin set password), mark the user's other unused invite and reset requests as used. When a User is rescoped to server scope, mark all of its unused requests as used. Both walk the user's requests within the longest validity window.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bcf75f76d88b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.