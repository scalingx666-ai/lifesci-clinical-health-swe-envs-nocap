# Issue

**Title:** TRUNK-6827: Keep the outbox from enqueueing events about its own rows (2.9.x backport)

## Description

Backport of the outbox part of #6637 ([TRUNK-6827](https://openmrs.atlassian.net/browse/TRUNK-6827)).

On 2.9.x, `EventInterceptor.onSave` runs for every insert, so saving an `OutboxEvent` publishes a `SaveDbEvent` about it. An `@OutboxEventListener` that accepts that event (one taking `SaveDbEvent<?>` or `EntityEvent<?>`, say) then makes `OutboxEventInterceptor` save another `OutboxEvent`, and so on until the heap runs out on the first create or update. `OutboxEventInterceptor` now ignores entity events about an `OutboxEvent`.

The rest of #6637 isn't needed here. Hibernate 5.6 calls `onSave` and `onDelete`, which this branch's `EventInterceptor` overrides, so create and delete events already reach it. `OutboxEvent` isn't `@Audited` on 2.9.x, so its Envers audit rows can't feed the loop either.

**Tests:**
- `OutboxEventInterceptorTest` is the same as on master. Without the check, the test that keeps events about an `OutboxEvent` out of the outbox fails.
- The api suite passes: 5485 tests, 0 failures.
- I also ran a temporary context-sensitive test with Envers on, an `@OutboxEventListener` taking `EntityEvent<?>`, and real commits. Without the check, creating a location, a patient or a global property runs out of heap. With it, each one commits and adds a handful of outbox rows (five for a location).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

[TRUNK-6827]: https://openmrs.atlassian.net/browse/TRUNK-6827?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3707c909e0da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.