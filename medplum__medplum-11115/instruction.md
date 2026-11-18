# Issue

**Title:** fix(react): only request login status for a login ID in SignInForm

## Description

SignInForm requests the status of the login named by its login prop. Only do so when the value is a UUID, and encode it in the request path.

Discovered by Anthropic's OSS Scanner, as vulnerability ANT-2026-1VVR6VW2

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4eab165d43f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.