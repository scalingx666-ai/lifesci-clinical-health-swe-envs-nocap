# Issue

**Title:** fix(cli): keep profile settings when MedplumClient clears storage

## Description

`FileSystemStorage.clear()` wrote `{}` to `~/.medplum/<profile>.json`. `MedplumClient` calls it on `signOut()` and on an unrecoverable 401, so any CLI command that hit an expired session erased the profile's base URL, client ID, etc. along with the tokens.

`clear()` now keeps the `options` entry and drops everything else.

Follow-up from #11213 (the in-memory storage there is still needed for partial-failure retries).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `163f121f3426`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.