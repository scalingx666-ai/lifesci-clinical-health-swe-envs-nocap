# Issue

**Title:** fix(backend): list all outgoing webhook endpoints, not just Svix's first page

## Description

## What does this change?

`GET /webhooks/endpoints` now returns every endpoint instead of only Svix's first page.

## Why?

The route called `svix_service.list_endpoints(app_id)` once and returned `result.data`, dropping the iterator, so with more than 50 endpoints (Svix's default page size) the rest were invisible. Endpoints can be created per user, so apps with per-user webhooks hit this quickly.

The walk lives in the route because `list_endpoints` is already a one-page helper whose docstring says to pass the iterator to get the rest. The loop and the repeated-iterator guard mirror what #1809 does for message listing. I kept the response a plain array so nothing changes for API consumers. I didn't add a `limit` to the Svix call since the default is fine and keeps this change minimal.

The fix was small enough that I went ahead with it, happy to change direction if you'd rather handle it differently.

## How did you test this?

Against the Svix server from `docker-compose.yml` (`svix/svix-server:v1.101.0`), one app with 60 endpoints:

```
single list_endpoints call (old route behavior)   50 endpoints, done=False
fixed route handler                               60 endpoints, 60 unique ids
```

New tests in `tests/api/v1/test_outgoing_webhooks.py`: the route follows the iterator across two pages and returns all endpoints in order, and it raises on a repeated iterator instead of looping. Both fail on main. The whole file passes (37 tests), ruff and ty are clean.

Not tested: the 60-endpoint check called the route handler directly against real Svix rather than going through HTTP with a developer token. The HTTP and auth path is covered by the existing mocked route tests.

## AI usage

Claude Code (Claude Opus) helped trace the bug, write the fix and tests, and draft this description. I reviewed the change and ran the checks above.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Outgoing webhook endpoint listings now include results from all available pages.
  * Webhook event-type synchronization and message-payload deletion now process results across all available pages.
  * Pagination stops when there are no more pages, and reports an error if the same page is returned repeatedly, preventing an endless fetch loop.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31761bbbcec1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.