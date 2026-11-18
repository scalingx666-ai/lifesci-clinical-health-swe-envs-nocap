# Issue

**Title:** feat(backend): exclude seed users from telemetry counts

## Description

## What does this change?

Users created by the [seed data generator](https://docs.openwearables.io/developer-portal/settings/seed-data-generator) get a new `user.is_seed` flag. [Telemetry](https://docs.openwearables.io/dev-guides/telemetry) leaves them and their data out of every count and reports them separately as `seed_users`.

## Why?

Seed users are regular `User` / `UserConnection` rows with real provider names, so an instance where someone clicked "Generate" looked like real Garmin/Oura adoption in the telemetry. The only marker was the `[SEED:...]` prefix in `first_name`. I didn't want to filter on that prefix, because it can be edited through the API. The migration still uses it once to backfill users seeded before this change.

## How did you test this?

Fresh DB, one real user created through `user_service`, then 5 users from the seed generator, payload from `build_payload`:

```
before seed: total_users "1-10", seed_users "0", active_connections "0", workouts_by_provider {}
after seed:  total_users "1-10", seed_users "1-10", active_connections "0", workouts_by_provider {}
```

The DB had 10 active connections and 500 event records at that point, all of them seed data. On main they would have been reported.

Query cost on Postgres 18 with 1M users / 1M active connections, 20 of the users seeded:

| query | before | after |
|---|---|---|
| `count_users` | 31 ms | 38 ms |
| `count_users_with_active_connection` | 205 ms | 129 ms |
| `count_seed_users` | - | 0.1 ms (index only scan on `ix_user_is_seed`) |

The seed filter is a `NOT IN` against the partial index, and Postgres runs it as a hashed SubPlan. The generator caps one run at 10 users, so that list stays small. On the same data the migration took 0.8 s and the backfill flagged exactly the 20 prefixed users.

## AI usage

Claude Code (Claude Opus 5.5) for the implementation and the perf check, reviewed by me.


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Telemetry now reports seed-user counts separately. Seed users and their associated connections and activity are excluded from other user, connection, and activity totals.
  * The telemetry payload is now version 2 and includes a `seed_users` count.

* **Documentation**
  * Updated the telemetry guide to describe the version 2 payload and how seed-user counts are reported.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `970bbfae18f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.