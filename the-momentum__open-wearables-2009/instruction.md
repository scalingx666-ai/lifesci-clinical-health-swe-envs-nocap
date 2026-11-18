# Issue

**Title:** fix(frontend): send a session the API refuses back to sign in

## Description

## What does this change?

When the backend refuses the session's access token (401), the portal renews the session once and retries; if the refresh is refused too, it clears the session cookie and redirects to `/login` instead of answering with a 500.

_(Added during review by Sebastian Kalisz:)_ A renewed token that the API refuses as well now clears the session cookie too. Before, the redirect left the cookie in place and `/login` sent the user straight back to the dashboard.

_(Added during review by Sebastian Kalisz:)_ The session is cleared only when the API refuses the refresh (4xx). When the refresh fails on an outage (5xx or no response), the request fails and the session stays, so the user is not signed out by a backend restart. This also applies to the scheduled refresh, which used to sign the user out on any refresh error.

## Why?

A session from another stack (different database or `SECRET_KEY`), from before a `SECRET_KEY` rotation, or of a deleted developer made every page fail with a 500, and `/login` bounced to `/dashboard` because a cookie existed - the only way out was clearing cookies by hand.

The handling sits in the API layer (via `getRequestEvent()`) rather than in each page or in `handleError`: `handleError` cannot redirect, and per-page handling would have to be repeated in the 74 loads, actions and endpoints that call `requireToken`. Retrying after a forced refresh instead of signing out straight away keeps a `SECRET_KEY` rotation from signing everyone out while their refresh tokens are still valid.

Things worth a look in review:
- A 401 on a token that is not the session's (sign-in, accept-invite) still surfaces as `ApiError`, so "Incorrect email or password" is unchanged.
- `describe()` and `optional()` now rethrow the redirect; otherwise a form would show "Something went wrong" and a dashboard card would fall back silently.
- The `+server.ts` JSON endpoints fetched from the browser get a 303 too, which that fetch cannot use. The cookie is cleared, so the next navigation lands on `/login`; I left those as they are.

Related issue: none

## How did you test this?

Two new e2e tests drive it through the mock API, which now refuses tokens it did not issue (`/__forget-tokens/all` = another stack, `/__forget-tokens/access` = rotated `SECRET_KEY`):

```
# signed in, then the API forgets every token; GET /login
Before (main): 500, server log "ApiError: Could not validate credentials"
After:         /login -> /dashboard -> /login, sign-in form shown, ow_session cookie gone

# signed in, then only the access tokens are forgotten; GET /users
Before (main): 500
After:         200 on /users, session renewed
```

Against the real backend in Docker (this branch's image, own Postgres), with a portal built from `main` and one built from this branch, both signed in:

```
# backend restarted with a different SECRET_KEY, same database; GET /dashboard
main: 500, "ApiError: Authentication required: provide JWT token or API key"
this: 200 - API log: GET /dashboard/stats 401, POST /token/refresh 200, GET /dashboard/stats 200

# backend on a fresh database; GET /login
main: 303 to /dashboard, then 500
this: /login -> /dashboard -> /login, sign-in form, ow_session cleared
      API log: GET /dashboard/stats 401, POST /token/refresh 401
```

Unit tests in `src/lib/server/server.spec.ts` cover the shared renewal for parallel calls and the give-up cases (refused refresh, no refresh token, renewed token refused again). `bun run check`, `eslint`, `prettier --check`, the server unit tests and the full e2e suite pass.

Not tested: a deleted developer (should take the fresh-database path, since its refresh token goes with it), and the browser-side fetches of the `+server.ts` endpoints.

## AI usage

Claude Code (Claude Opus 5.5) wrote the fix and the tests and drafted this description; I reviewed the approach and the result.

## Breaking change

None for the API or deployments. A session the API no longer accepts and cannot renew is cleared, so its user signs in again. The browser-side fetches of `+server.ts` endpoints get the 303 too; they fail once and the next navigation lands on `/login`.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Rejected access tokens can trigger a session renewal and one request retry, helping users continue without interruption.
  * If a session cannot be renewed, users are returned to the sign-in page and their session cookie is cleared.
  * Redirects to sign-in now work consistently when triggered during form submissions or optional operations.
  * Navigation remains available after an access token is forgotten, while sessions with rejected tokens correctly return to sign-in.
  * Added coverage for token renewal, request retries, and sign-in behavior when tokens are rejected.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8adb8d0b2fff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.