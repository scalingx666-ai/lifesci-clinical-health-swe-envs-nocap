# Issue

**Title:** TRUNK-6827: Forward onPersist and onRemove through ChainingInterceptor

## Description

Fixes [TRUNK-6827](https://openmrs.atlassian.net/browse/TRUNK-6827).

`ChainingInterceptor` now overrides `onPersist` and `onRemove` and forwards them to each chained interceptor. Hibernate's defaults for those delegate to `onSave` / `onDelete`, so interceptors that implement only the deprecated pair are still invoked exactly once. That covers core's `AuditableInterceptor`, `DropMillisecondsHibernateInterceptor`, `GlobalPropertyCacheInterceptor` and `RolePrivilegeCacheInterceptor`, as well as module interceptors like openmrs-module-event's.

The chain's own `onSave` / `onDelete` now delegate to `onPersist` / `onRemove`, so either entry point reaches every interceptor once. It also forwards `onInsert`, `onUpdate`, `onUpsert`, the 4-argument `onDelete`, and `preMerge` / `postMerge`, which Hibernate 7 calls and the chain was dropping. `EventInterceptor.onRemove` gets its missing `@Override`.

In a create event, the entity id is still null, because Hibernate calls `onPersist` before the id is assigned. That was already the case with `onSave`.

**Outbox:** with create events published, the transactional outbox could loop on its own rows, as it already does on 2.9.x. Saving an `OutboxEvent` publishes a `SaveDbEvent` about it, so an `@OutboxEventListener` that accepts that event (one taking `SaveDbEvent<?>` or `EntityEvent<?>`, say) made `OutboxEventInterceptor` save another `OutboxEvent`, and so on, until the heap ran out on the first create or update. Two changes stop it:
- `OutboxEventInterceptor` ignores entity events whose entity is an `OutboxEvent`.
- `OutboxEvent` is no longer `@Audited`, as on 2.9.x. With Envers on, each outbox row's audit row is published as a `SaveDbEvent<HashMap>`, which the check above can't recognise, so it went into the outbox as another row with an audit row of its own. `EnversAuditTableInitializerDatabaseIT` now treats an entity as audited only when its own class is `@Audited`, because Envers doesn't audit `OutboxEvent` through `BaseOpenmrsObject`'s annotation.

**Tests:**
- `EventInterceptorTest` covers create, update and delete through the real session factory. On master, create and delete fail (`expected: <1> but was: <0>`), while the update control passes.
- `ChainingInterceptorTest` checks that legacy-only and new-only interceptors are each called exactly once from both entry points, that "state modified" results are combined, and that the stateless and merge callbacks are forwarded.
- With only `ChainingInterceptor` reverted, 8 of these 9 tests fail.
- `OutboxEventInterceptorTest` checks that events about an `OutboxEvent` stay out of the outbox while others go in. The first test fails without the check.
- The full default api suite passes: 5458 tests, 0 failures.

**Runtime:** I ran this change on MySQL 8 (`mvn jetty:run`) with all 31 O3 reference application modules upgraded to Platform 3. All of them start, and logging in works. Creating and updating a location over REST works, with `creator`, `date_created` and `changed_by` populated, so the deprecated-API interceptors still run through the chain.

I also ran it on MySQL 8 with only the REST module, `hibernate.integration.envers.enabled=true` and a temporary `@OutboxEventListener` taking `SaveDbEvent<?>`. Creating a location over REST returns 201 and adds five outbox rows. With `@Audited` put back on `OutboxEvent`, logins fail and so does the outbox poller, with `Data too long for column 'payload'`, because each outbox row nests the previous one until the payload outgrows the MEDIUMTEXT column.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Fp7T1pGYEMrMVp1M7AW9Fg

[TRUNK-6827]: https://openmrs.atlassian.net/browse/TRUNK-6827?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34dc604e6eea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.