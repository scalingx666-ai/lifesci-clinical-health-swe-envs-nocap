# Issue

**Title:** perf(backend): cache provider access tokens for the duration of a sync

## Description

Cache provider access tokens on the database session for the duration of a sync, so repeated provider requests no longer re-read the user connection for every call. Stacked on top of the connection failure reporting changes.

## Changes

- Cache a fresh provider access token per session and per user/provider; tokens close to expiry are dropped from the cache and refreshed as before.
- Reload only the token columns when reading the connection, so a token refreshed by another worker is seen even when the connection is already loaded in the session.
- When a provider rejects a token with 401 (both for regular requests and binary downloads), re-read the token once and retry if another worker has refreshed it in the meantime.
- Always read a fresh token for the Garmin deregistration grant check, so a stale cached token cannot cause an active connection to be revoked.

## How I tested

- I ran the local Docker stack (Postgres, Redis, API, Celery worker) built from this branch on a fresh database.
- I created test users and provider connections in the local database, and set up each token state there directly: valid, close to expiry, expired, missing refresh token, and changed from a separate database session to stand in for another worker.
- Provider traffic went to a local mock of the provider APIs. The mock accepted or rejected tokens as each scenario required. No request reached a real provider, and no real token was refreshed or revoked.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

## Bug Fixes

* Provider connections now reuse valid access tokens briefly, reducing repeated token checks. When a provider rejects a token, requests retry once if a newer token is available; requests are not retried if the token is unchanged.
* Garmin grant checks now use the latest available token, helping avoid treating an active connection as stale when credentials have been refreshed elsewhere.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41b990f17dbe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.