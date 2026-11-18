# Issue

**Title:** fix(server): apply each subscriber's token scopes to WebSocket subscription notifications

## Description

WebSocket subscription notifications are now evaluated against each bound subscriber's own token, including its SMART scopes, before they are sent. This uses the same `canPerformInteraction` read check as a normal FHIR read, so what a subscriber receives over a WebSocket matches what it could read over the REST API with the same token.

Previously, the subscription worker's check was based on the stored access policy of the membership that most recently bound to the subscription, which does not account for a token's SMART scopes or for multiple sockets bound to the same subscription.

## Changes
- `ws/subscriptions.ts`: per-socket read check before sending a notification, including the resource referenced by a Binary's `securityContext`, with a debug log when a notification is skipped. The per-subscriber work is split out of `sendSubscriptionEventNotifications` into smaller functions.
- `ws/subscriptions.test.ts`: tests for access policy restrictions, token scopes, token scopes with criteria, Binary security context, and a positive case where a scoped token still receives matching resources

## Compatibility
Logins using the default `openid` / `offline` scopes (including the Medplum app and most `MedplumClient` usage) are unaffected. Apps that request narrower resource scopes should request read access for every resource type they subscribe to.

## Testing
- `npx vitest run src/ws/subscriptions.test.ts src/fhir/operations/getwsbindingtoken.test.ts src/workers/subscription.test.ts`: 132 passed, 2 skipped

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `96d19bef8972`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.