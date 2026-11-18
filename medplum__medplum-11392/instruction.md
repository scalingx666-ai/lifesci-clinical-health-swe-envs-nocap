# Issue

**Title:** fix(server): apply access policy hidden fields and SMART scopes to /auth/me profile

## Description

/auth/me now removes the AccessPolicy hidden fields from the profile. For logins with SMART resource scopes, the profile is reduced to resourceType and id when the effective policy does not allow reading it, matching /oauth2/userinfo. Logins without resource scopes still receive their profile when their AccessPolicy does not grant the profile type.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `564ed95b4c13`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.