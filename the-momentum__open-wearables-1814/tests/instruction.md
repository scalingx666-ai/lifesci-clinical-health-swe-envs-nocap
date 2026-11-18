# Issue

**Title:** fix(backend): refresh expired token before provider deregistration

## Description

## What does this change?

Provider deregistration on disconnect and on user delete now goes through `get_valid_token`, so an expired access token gets refreshed before we call the provider. No retry on 401 - refreshing up front should be enough.

## Why?

I disconnected a Garmin user on our test instance and the deregistration call came back with a 401. We revoked the connection locally anyway, but the app was still listed under connected apps in the user's Garmin Connect settings, Garmin kept pushing data for that user for hours (all rejected with `not connected`), and the `deregistrations` webhook never arrived.

Cause: Garmin is push-based, so after the initial backfill we never call its API and the stored access token just expires. Disconnect sent that stale token to `DELETE /user/registration`. With a fresh token the deregistration goes through and Garmin sends `deregistrations` about 4 s later.

Side effect handled here: if the refresh token itself is rejected, `refresh_access_token` revokes the connection before `disconnect` runs, and `disconnect` then skipped the row (it only updated non-revoked ones), leaving tokens in the DB. `disconnect` now clears tokens on an already revoked connection too; the status change and the `connection.revoked` event behave as before.

Tests: `UserConnectionFactory` defaulted `token_expires_at` to 2025-12-31, so factory connections now have expired tokens and disconnect tests would additionally call Garmin's token endpoint. The default is now one day ahead. Disconnect tests still hit Garmin's real API for the deregistration call itself - that's #1813.

## How did you test this?

On our test instance, before the fix (Garmin user connected for ~4 weeks):

```
22:12:20 Failed to deregister user from provider API: Client error '401 Unauthorized' for url 'https://apis.garmin.com/partner-gateway/rest/user/registration'
22:13 - 06:56  27 Garmin push webhooks for the same user -> "User ... not connected", no deregistrations webhook
```

After reconnecting (fresh token) and disconnecting again:

```
13:52:30.03 Deregistered user from provider API
13:52:30.05 Connection revoked (user_disconnected)
13:52:33.96 Received Garmin webhook {"deregistrations": 1}
```

Added tests for: expired token refreshed before deregistration (service + API), valid token used as-is, refresh failure skipping deregistration without breaking disconnect, and tokens cleared when the refresh is rejected. Not tested against a real expired Garmin token with this branch deployed.

## AI usage

Claude Code (Opus 5.5) for digging through Railway logs and drafting the fix and tests.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Disconnecting a provider now clears stored tokens even when the connection was already revoked.
  * Provider deregistration uses a refreshed access token when the stored token has expired. If refreshing fails, disconnect still completes and clears the connection’s tokens.

* **New Features**
  * Added a public way to retrieve a valid provider access token for requests made outside standard authenticated requests.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a8c59af9c14a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.