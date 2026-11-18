# Issue

**Title:** fix(backend): add server-side lifetime for developer refresh tokens

## Description

> _Added during review by Sebastian Kalisz._

## ⚠️ Breaking change

A developer refresh token whose `created_at` is older than `DEVELOPER_REFRESH_TOKEN_EXPIRE_DAYS` (default 30) is refused on `POST /api/v1/token/refresh` with `401 Invalid or revoked refresh token`. Tokens rotate on every refresh, so this is an idle timeout. It applies on upgrade to tokens issued before it, too; no migration.

| Who | Effect |
|---|---|
| Portal users | None: the session cookie already expires 30 days after the last refresh, the same moment as the token. |
| API clients signed in as a developer | A refresh token left unused for more than 30 days stops working; sign in again, or raise the setting. |
| SDK tokens | Not affected. |

---

- Add DEVELOPER_REFRESH_TOKEN_EXPIRE_DAYS setting (default 30 days) matching the portal session
- Enforce lifetime in RefreshTokenRepository.claim_valid_token during token rotation
- ~~Support revoking refresh tokens in POST /api/v1/auth/logout when payload is provided~~ _(Changed during review by Sebastian Kalisz:)_ dropped: `POST /api/v1/token/revoke` already revokes a refresh token and is what the portal uses on sign-out; logout is unchanged.
- Add unit tests for developer token expiry, rotation, and ~~logout revocation~~
-

<!--

Don't describe the diff - we can read that. Tell us what we can't read: why this
approach, what you ruled out, what you checked, what you're still unsure about.

Use whatever tools help you write it, but do the editing yourself. AI writes far more
than it needs to - cut it down to the few sentences that actually say something.
-->

## What does this change?

<!-- A sentence or two. -->

## Why?

<!-- What problem does this solve, and for whom? If you considered another approach, tell us why you didn't take it. -->

Related issue: #

## How did you test this?

<!--
Be concrete: the commands you ran, the flow you clicked through, the data you looked at.
Best formats: before/after request + response, a table with numbers, a screenshot for
docs/UI. Say what you did NOT test. Examples: contributing/pull-requests.md#showing-that-it-works

If your change touches a provider integration, we need to know it was tested against
a real account and real API responses.

Paste the proof where you can - a log excerpt, a screenshot, a sample response - with
all secrets and sensitive personal data removed.
-->

## AI usage

<!-- Which tools and models you used, and roughly what for. "None" is a perfectly good answer. -->

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Developer refresh tokens now expire after 30 days by default. The expiration period can be configured.
  * Expired developer refresh tokens can no longer be used to obtain new tokens; this age limit does not apply to SDK refresh tokens.
* **Documentation**
  * Logout guidance now directs clients to revoke refresh tokens through the token revocation endpoint.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ca121dd4e48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.