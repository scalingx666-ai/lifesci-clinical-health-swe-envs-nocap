# Issue

**Title:** fix(frontend): show a notice instead of a 500 when outgoing webhooks are off

## Description

## What does this change?

`/webhooks` now checks `outgoing_webhooks_enabled` from `/api/v1/config` before loading subscriptions. When it's off, the page shows a notice pointing to `OUTGOING_WEBHOOKS_ENABLED` and the [webhooks guide](https://openwearables.io/docs/api-reference/guides/webhooks), and `/webhooks/:id/deliveries` redirects back to `/webhooks`.

## Why?

With webhooks off (the default), `/api/v1/webhooks/endpoints` returns 503 and the new SvelteKit loader turned that into a 500 page. The React dashboard checked `/config` first and showed a notice instead, so this was a regression from #1530.

## How did you test this?

Locally with `OUTGOING_WEBHOOKS_ENABLED=false`:

- Before: `GET /webhooks` -> 500, frontend log `ApiError: Outgoing webhooks are not enabled ...` from `+page.server.ts`

<img width="1366" height="930" alt="1" src="https://github.com/user-attachments/assets/27d8999c-7488-44c9-bea1-d83e22ba5b33" />


- After: notice is shown, "New subscription" is disabled

<img width="1451" height="864" alt="image" src="https://github.com/user-attachments/assets/0af3d93f-4a5d-4c1a-9657-015a0f96eeff" />

Added two e2e cases to `webhooks.e2e.ts`. The mock API got a `__webhooks-off` switch that, like the backend, answers 503 on `/webhooks/endpoints*`, so the old loader would fail these tests.

## AI usage

Claude Code (Claude Opus 5.5) for finding the cause in logs, the fix and the tests.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * The webhooks page now reflects whether outgoing webhooks are available on your instance, explains when they’re disabled, and links to setup guidance.
  * Subscription creation is unavailable while webhooks are disabled, and delivery pages redirect to the webhooks overview.

* **Bug Fixes**
  * Feature availability is now consistently shown across the app, including when configuration can’t be retrieved.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e093cedddbf5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.