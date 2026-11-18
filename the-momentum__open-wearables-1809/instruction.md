# Issue

**Title:** feat(backend): delete a user's outgoing webhook payloads from Svix on user deletion

## Description

## What does this change?

Deleting a user now also deletes the payloads of their outgoing webhook messages from Svix. A Celery task, queued after the DB delete, finds the user's messages through the `user.{user_id}` channel in every developer's Svix app and deletes their payloads with `bulk-expunge`.

## Why?

`DELETE /api/v1/users/{user_id}` removed the user's rows from our DB but left their webhook payloads (heart rate, sleep, workouts) in Svix for up to 90 days. For anyone using OW to handle a GDPR erasure request, Svix was the one place the data survived.

Some choices worth knowing about:
- It runs as a background task, not inside the request: a user can have thousands of messages across several apps. The task retries up to 5 times, and deleting a payload twice is harmless.
- It is queued with a 60 s delay, so webhook sends already queued for this user reach Svix first and get covered. A send stuck in a longer backlog would be missed.
- If queuing fails (e.g. Redis down), we log a warning and the user deletion still succeeds, same as the Redis lock release in that method.
- On svix-server older than 1.101.0, where `bulk-expunge` doesn't exist, it falls back to deleting payloads one at a time.

Not covered: Svix has no API to delete message records, only their payloads. The records stay, and their event id contains the user id (e.g. `timeseries.<user_id>...`). Worth stating on the compliance page (#1436). Point 1 of the issue (configurable payload retention) is in #1719.

Related issue: #1610

## How did you test this?

Full flow on a local stack (API + Celery worker from this branch, svix-server v1.101.0):

1. `POST /api/v1/settings/seed` with 1 user: the worker emitted 3 `workout.created` and 2 `sleep.created`, stored in Svix with full payloads.
2. `DELETE /api/v1/users/{user_id}` → 200.
3. 60 s later the worker ran the task: `{'deleted': 5, 'errors': []}`.
4. All 5 messages are still listed in Svix, each payload now `{"expired": true}`.

## AI usage

Claude Code (Claude Opus) wrote the implementation and tests; I reviewed them.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Webhook message payloads for deleted users are removed in the background across developer applications. Cleanup handles large message histories and may retry if an application cannot be processed.
  * User deletion still completes if cleanup cannot be scheduled. Cleanup is not scheduled when webhooks are disabled.
* **Documentation**
  * Webhook delivery guidance now explains cleanup timing and limitations, including that delivery history remains while payloads are removed, and that older payloads may remain until retention expires.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32f8bc201eb3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.