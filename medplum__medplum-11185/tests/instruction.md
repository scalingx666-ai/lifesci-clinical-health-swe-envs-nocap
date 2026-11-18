# Issue

**Title:** fix(server): resolve token exchange identity like the external auth callback

## Description

Token exchange mapped external claims to a user with only the legacy useSubject flag, so identitySource and identityMappingMode were ignored. It now uses resolveExternalLoginIdentity, the same function as /auth/external, so both flows agree on the user. IdP configurations the callback rejects are now also rejected by token exchange.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e74669dbccbe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.