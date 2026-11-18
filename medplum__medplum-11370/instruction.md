# Issue

**Title:** Strip ClientApplication secret from auth me responses

## Description

`GET /auth/me` includes the caller's profile read through the system repository. When that profile is a ClientApplication, the response currently includes its stored client secret.

Explicitly remove `ClientApplication.secret` from a copy of the response profile. Strengthen the existing ClientApplication test to check that the profile is returned without a secret and the stored credential remains intact.

Validation: Prettier and ESLint pass (one existing Bowser warning). Integration tests were attempted but local Redis/PostgreSQL are unavailable. Server type checking reports two existing missing `isValidCronString` exports in validation.ts and cron.ts; no errors in the changed files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d6bd6e728a95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.