# Issue

**Title:** chore(server): log bots that run as a caller with SMART scopes

## Description

Adds diagnostic logging for bots that run as the caller's own ProjectMembership when the caller's login has SMART resource scopes (`patient/`, `user/`, `system/`) or a SMART App Launch context. The bot's access token does not carry those scopes, so they do not limit the bot. No change to what the bot can access.

## Changes
- `BotExecutionRequest` has an optional `callerLogin` (`scope` and `launch`), set when the bot runs as the caller's own membership, and an optional `entryPoint`.
- `$execute` and custom operations pass the caller's login when the bot runs as the caller's membership; `/cds-services/:id` and agent transmits always run as the caller and always pass it.
- `executeBot` logs `Bot ran as a caller with SMART scopes` with the bot, project, caller membership and profile, scope string, launch reference, and entry point. Throttled per project, bot, membership, entry point and scope (10 minute window).
- The bot's Login and token are unchanged (`openid`, no launch).

## Compatibility
Access is unchanged. Bots get the same token as before; this only adds a warning log line.

## Testing
- New tests in `bots/utils.test.ts`, `fhir/operations/execute.test.ts`, `fhir/operations/custom.test.ts`, `cds/routes.test.ts` and `ws/agent.test.ts` assert that the bot token keeps `openid`, that access is unchanged, and that the log fires (or doesn't) as expected.
- `npx vitest run src/bots src/cds src/ws/agent.test.ts src/fhir/operations/execute.test.ts src/fhir/operations/custom.test.ts`: 117 passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7e7e4019144`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.