# Issue

**Title:** chore(server): log subscription notifications that include Binary.data

## Description

Logs subscription notifications that include inline `Binary.data`, to find subscribers that rely on it before notifications stop including it. Notifications are unchanged.

## Changes

- The subscription worker logs a warning, `Subscription notification includes Binary.data`, when a rest-hook, Bot or WebSocket notification carries a Binary with inline `data`. The log includes the Binary id, project, channel and subscription ids.
- The warning goes through `LogThrottle`: it is logged once per project, channel and subscriptions every 10 minutes, with the number of suppressed occurrences.
- Notifications for Binaries without inline `data` (for example, raw uploads) are not logged.

## Compatibility

- No behavior change.

## Testing

- `workers/subscription.test.ts`: rest-hook and WebSocket notifications for a Binary created with inline `data` still include `data`, and log the warning with `suppressed: 0`.
- Ran the subscription worker, dispatch and WebSocket subscription suites.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a8d70aa5e644`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.