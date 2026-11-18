# Issue

**Title:** fix(backend): revoke grants rejected at the provider

## Description

## What does this change?

Connections that can no longer sync stop being synced forever:

- A 401 for a token nobody refreshed in the meantime forces one refresh. If the provider rejects the refresh token, the user revoked us at the provider: the connection is revoked and the sync ends as `reauth_required`, with no retries. If the refresh works, the request is retried once, and another 401 means only that endpoint is refused.
- A connection that gets nothing but 401/403 for a day is revoked. This covers providers without refresh tokens (Polar) and lapsed Oura memberships (Oura's 403). One successful response resets the count, so endpoints a healthy grant can't use never add up to a revoke.
- Celery task results expire after an hour instead of three days. Nothing reads them, and they share the broker's Redis.

## How did you test this?

Unit tests for each case: refresh and retry, rejected refresh, 401 after a successful refresh, no refresh token, a day of failures, a success resetting the count, unflushed connection changes kept. Full backend suite passes.

## Breaking change

- Connections in these states become `revoked` on their next sync and each sends a `connection.revoked` webhook, so expect a batch of them right after the upgrade. The user has to reconnect.
- Celery task results are kept for an hour instead of three days.


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Improved recovery when a connected service rejects an expired access token. The app can refresh credentials and retry the request, while avoiding unnecessary retries when refresh credentials are unavailable or the refreshed request is still rejected.
  * Connections with repeated authentication failures over at least a day are now revoked and require users to reconnect. Successful requests clear the failure status, and recovery works across regular API requests and file downloads.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4066be3c64cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.