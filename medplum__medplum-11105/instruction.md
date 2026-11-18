# Issue

**Title:** fix(server): revoke all of a user's logins when the password is set

## Description

setPassword revoked only the first page of the user's Logins. Walk all of them with processAllResources and patch the ones that are not already revoked.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fce7a9045ce7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.