# Issue

**Title:** fix(backend): ignore stale Garmin deregistration pings after reconnect

## Description

## What does this change?

Before revoking a Garmin connection on a deregistration ping, we now ask Garmin whether the connection's current token still works (`GET /partner-gateway/rest/user/id`, refreshing the token first if it expired). If Garmin answers with the same `userId`, the ping belongs to an old grant and is ignored. Any other outcome revokes as before.

## Why?

Garmin keeps the same `userId` across re-authorizations, and the deregistration ping carries nothing else (no timestamp, no token). A user who disconnects and reconnects can get the new connection revoked by the ping for the old grant, observed 45 min later in #1803. Asking Garmin is the only reliable signal, and it only changes the outcome when Garmin itself confirms the grant is active. A fresh ping after our own `DELETE /registration` still gets a 401 and revokes.

Some details:
- I had to add a `revoke_on_failure` flag to `get_valid_token` / `refresh_access_token`, because the check refreshes the token first and a failed refresh revokes the connection on its own, with `reason="refresh_failed"`. Push tokens are almost always expired by the time Garmin deregisters a user, so most real deregistrations would have reached integrators as `refresh_failed` instead of `deregistration`. The check passes `False` and the deregistration handler revokes with the right reason. All other callers keep the default.
- A ping for an already revoked connection is now skipped. Our own disconnect already sends `connection.revoked` with `reason="user_disconnected"`, and the ping that follows used to send a second one.
- A Garmin error, network error or Redis lock timeout during the check revokes, same as before.
- Deregistrations are processed in Celery, so the extra calls don't count against Garmin's 30 s webhook timeout.

Related issue: #1803

## How did you test this?

I couldn't reproduce the delayed ping: on our test instance it arrived ~4 s after deregistering. I decided to ship the change anyway, because Garmin gives no guarantee about when it sends the deregistration ping, so a late one after a reconnect can happen at any time.

## AI usage

Claude Code (Claude Opus) wrote the implementation and tests; I reviewed them.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Garmin deregistration notifications no longer revoke a connection when Garmin confirms its grant is still active. Stale notifications are ignored, while invalid or mismatched grants continue through the revocation process.
  * Token refresh failures can be handled without automatically revoking a connection when appropriate. Default behavior remains unchanged.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32f0735d526b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.