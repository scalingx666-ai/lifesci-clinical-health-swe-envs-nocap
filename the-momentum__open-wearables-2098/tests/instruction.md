# Issue

**Title:** feat: OAuth redirect allowlist

## Description

# **Breaking changes**
- a `redirect_uri` outside the allowlist gets `400`: add your domain to `OAUTH_REDIRECT_ALLOWLIST`
- failures now also land on `redirect_uri`: check `status`, don't assume arriving there means connected
- `provider` / `status` / `message` are appended to `redirect_uri`'s query, overwriting same-named params
- disabled providers get `400` at `authorize`; an invalid state or failed token exchange in the callback is a `303` redirect, not a `4xx` JSON response

## What does this change?

- `redirect_uri` on `/oauth/{provider}/authorize` must match `OAUTH_REDIRECT_ALLOWLIST` (default the Connect app's `openwearables://oauth/callback`), the dashboard origin (`FRONTEND_URL`) or `CORS_ORIGINS`; anything else gets `400`. Closes the open redirect in the callback.
- Disabled providers are refused at `authorize` (`400`).
- The callback returns to `redirect_uri` on success **and on failure**, adding `provider`, `status` (`success` / `error`) and, on error, `message`, so an app's sign-in sheet never ends on JSON.
- Docs: quick integration note, docker variables, openapi.json.

Stacked on #2093, which makes `authorize` require a credential.

## Why?

Open-redirect half of #1979: the callback sent a 303 to whatever `redirect_uri` the flow was started with, so a genuine provider sign-in could end on an attacker's page.

The first commit is cherry-picked from the Connect app stack

Generated with help of Claude Code (Opus 5.5)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * OAuth sign-in can return users to approved web or app destinations, including the default app callback. Administrators can configure additional destinations.
  * OAuth returns include the provider and a success or error status; errors may include a message. The pairing result page shows whether the connection succeeded and displays available error details.
* **Bug Fixes**
  * Disabled providers and unapproved redirect destinations are rejected. When no destination is specified, the existing in-app success behavior remains.
* **Documentation**
  * Updated integration and deployment guides with redirect requirements, configuration, and callback parameters.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c26f0e0a2838`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.