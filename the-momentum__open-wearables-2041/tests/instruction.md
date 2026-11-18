# Issue

**Title:** fix(backend): confirm Strava webhook deletions and deauthorizations in the Strava API

## Description

Strava signs webhook events with a key it does not share, so anyone who knows an athlete ID could send a fake event that deletes a user's activities or disconnects their account. Before deleting or disconnecting anything, we now check the event against the Strava API with the athlete's own token. This also fixes deauthorization handling: Strava reports a deauthorization as an athlete update, which we used to ignore.

Part of ENG-1868 (#1978).

## Changes

- **Activity deletion:** an activity is deleted only after Strava confirms it is gone. If Strava still returns the activity, the event is ignored and a warning is logged. If we never stored the activity, the event is ignored without calling Strava.
- **Deauthorization:** we now handle the event Strava actually sends, an athlete update with `authorized: "false"`. Strava never sends the athlete delete event we used to listen for, so that handler was removed. The connection is revoked only when Strava rejects both the access token and the refresh token. A token rejected once, after which a refresh still works, is not enough.
- ~~**Revocation of deauthorized connections:** the connection is revoked with reason `deregistration` instead of `refresh_failed`, and its stored tokens are cleared. The authenticated API request helper gained an option that lets the caller revoke the connection itself, with its own reason.~~
  _(Changed during review by Sebastian Kalisz:)_ The connection is revoked through the shared `revoke_connection` with reason `deregistration`, like Garmin's deregistration; its tokens are no longer used and stay as they are. The API client's `revoke_on_failure` option stays, so the client doesn't revoke it first with another reason.
- ~~**Token endpoint failures:** when a token refresh fails because the provider is down (5xx) or rate-limited (429), the webhook delivery is now retried. These failures used to be reported as 400, so the delivery was dropped. This applies to all providers.~~ _(Removed during review by Sebastian Kalisz: main already raises these as retriable provider errors.)_

## How did I test it

- set up a test Strava API application and connected a test athlete account to it
- created a push subscription pointing to a temporary capture server
- created an activity, deleted it, and then deauthorized the app from the athlete's Strava settings

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Strava activity deletions are confirmed with Strava before stored activity data is removed; activities that still exist are retained.
  * Strava deauthorization events now revoke the connection when authorization is confirmed as invalid. Temporary API failures can be retried without removing the connection.
  * Authentication failures can leave connection revocation to the caller. Rate-limit and server errors during token refresh retain their original status.
* **Documentation**
  * Clarified webhook revocation reasons for Strava deauthorization and refresh failures.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4428ef76fc0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.