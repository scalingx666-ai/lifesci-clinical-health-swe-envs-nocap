# Issue

**Title:** fix(server): require an unscoped login for account self-service routes

## Description

The account self-service routes now require a login without SMART resource scopes, alongside the existing requirement for a non-On-Behalf-Of `User` login. A login with SMART resource scopes is granted access to specific FHIR resources, and account settings are managed from a regular session.

## Changes
- `auth/utils.ts`: add `hasSmartResourceScopes(login)`. `getCallerUserReference()` rejects logins with SMART resource scopes.
- `auth/me.ts`: `/auth/me` omits the `security` section for logins with SMART resource scopes. The rest of the response is unchanged.
- `docs/auth/how-mfa-works.md`: note the login requirement for the self-enrollment flow.
- Tests in `auth/utils.test.ts`, `auth/mfa.test.ts` and `auth/me.test.ts`.

## Compatibility
Logins without SMART resource scopes are unchanged. That includes `openid`, `profile`, `email`, `fhirUser`, `offline_access` and launch context scopes, so it covers the Medplum app, `MedplumClient` password login, external identity providers and refresh tokens.

Apps whose login requests resource scopes, including wildcard scopes such as `user/*.*`, and that also show account settings pages, should use a login without resource scopes for those pages.

## Testing
- `npx vitest run src/auth/utils.test.ts src/auth/mfa.test.ts src/auth/me.test.ts src/auth/changepassword.test.ts src/auth/revoke.test.ts`: 124 passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1d205f2d989`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.