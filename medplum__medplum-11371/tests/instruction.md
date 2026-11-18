# Issue

**Title:** Respect on-behalf-of identity in auth me responses

## Description

`GET /auth/me` currently returns the authenticating caller's profile, membership, and configuration even when the request acts on behalf of another membership, while its access policy already reflects that effective identity.

Use the authenticated context's effective project and membership for the response. Omit user-account and security/session details on delegated requests, since delegation does not grant account management access. Direct requests retain their existing behavior.

Add regression cases for a service client acting on behalf of a Patient within its project and a super-admin acting across projects. Check the effective profile, membership, project, configuration, access policy, and absence of account/security details.

This PR is independent of the separate ClientApplication secret-removal change.

Validation: Prettier and ESLint pass (one existing Bowser warning). Integration tests are blocked by unavailable local Redis/PostgreSQL. Server type checking reports existing missing `isValidCronString` exports in validation.ts and cron.ts; no errors in the changed files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d44b597e673`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.