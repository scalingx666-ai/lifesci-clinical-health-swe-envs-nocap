# Issue

**Title:** fix(server): apply SMART scopes to project admin rules

## Description

SMART scopes now also apply to the project admin access policy rules, and project admin resource types are only covered by scopes that name them. Super admin logins with SMART resource scopes or a SMART App Launch are not supported.

## Changes
- `getAccessPolicyForLogin()`:
  - Applies the project admin rules before the SMART scopes, so the scopes also limit them.
  - Refuses super admin logins that have `patient/`, `user/` or `system/` scopes or a SMART App Launch context (`SMART scopes are not supported for super admin logins`). This function runs when a login is bound to its project, for `client_credentials`, and for each authenticated request, so it covers every grant type.
- `fhir/smart.ts`: project admin resource types (`Project`, `ProjectMembership`, `User`, `AccessPolicy`, ...) are only covered by scopes that name them, such as `user/ProjectMembership.rs`. A wildcard scope (`user/*.cruds`) does not match them, and a wildcard policy entry is not expanded into them.
- Project admins keep their admin privileges; admin routes are unchanged.
- Docs: a note on the SMART scopes page.

## Compatibility
- Super admin tokens with SMART resource scopes or a launch context are refused: `client_credentials` returns an error, interactive logins cannot complete, and existing tokens are rejected.
- Project admin tokens with wildcard SMART scopes (for example `system/*.*`) no longer reach project admin resource types over the FHIR API unless a scope names them. Tokens without SMART resource scopes are unchanged.
- Non-admin tokens with SMART scopes read `AccessPolicy` only with a scope that names it.

## Testing
- New tests in `fhir/smart.test.ts`, `fhir/accesspolicy.test.ts` and `oauth/token.test.ts`. They fail on `main` and pass with this change, except the unscoped super admin case and the non-admin case, which pass on both; the non-admin case fails if the wildcard policy change is removed.
- Full server suite (`npx vitest run`): 5200 passed. The failures were suites that need a local shard database, plus two tests that timed out in the parallel run and pass when run alone.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6f7a2f8e193`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.