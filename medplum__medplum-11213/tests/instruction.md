# Issue

**Title:** feat(cli): add `medplum logout` command

## Description

## Summary

Adds a `medplum logout` command that fully invalidates the CLI's stored tokens.

- For every session stored in the profile (`activeLogin` plus the `logins` list), calls `POST /oauth2/logout`. The server marks the `Login` as revoked, so both the access token and the refresh token stop working. Expired access tokens are refreshed first, so the refresh token is revoked too.
- Removes the tokens from `~/.medplum/<profile>.json` and keeps the profile's settings (base URL, client ID, and so on).
- Tokens the server already rejects are reported as "Session already invalid" and removed.
- If any revocation fails for another reason (for example, a network error), the command exits non-zero and leaves stored tokens in place so it can be retried.

### Supporting change in `createMedplumClient`

- Accepts `storage` and `onUnauthenticated` overrides. Logout uses an in-memory client because `MedplumClient` clears its whole storage on a 401, which would otherwise erase the profile file's settings.
- No longer discards the stored `activeLogin` when a custom storage is passed, so a failed logout doesn't lose a token before it is revoked.

### Docs

Documents `logout` in `packages/docs/docs/cli/index.md`, including that stored client credentials are not removed (use `medplum profile remove`).

## Testing

- New tests in `auth.test.ts` (revokes all sessions and keeps settings, already-invalid tokens, failure keeps tokens, not logged in) and `util/client.test.ts` (custom storage keeps the stored session).
- `packages/cli`: 224/224 tests pass on Node 24; eslint and prettier clean.
- Not yet tried against a live server.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2415eeb7d3f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.