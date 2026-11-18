# Issue

**Title:** fix(server): do not cache resources read from the reader

## Description

`readResourceFromDatabase` writes every resource it reads to the Redis resource cache with `force: true`, regardless of which database pool served the read. If that read came from a replica that has not caught up, the stale row is cached for 24 hours.

For example:

1. A resource is deleted. The delete clears its cache entry.
2. A read of that resource is served by a lagging reader, which still has the row.
3. The stale resource is cached. Later reads, including writer-backed reads, return it from the cache until the entry expires.

The same applies after an update when `cacheResourcesOnWrite` is `false`, since updates then clear the cache entry instead of rewriting it.

GraphQL queries already run on the reader, and their reference lookups go through `readReferences` → `readResourceFromDatabase`, so this can happen today. #11142 would add another path (read-only batches on the reader).

## Change

Only write to the cache in `readResourceFromDatabase` when the read was served by the writer. The check uses the mode of the connection for the shard that served the read, not `Repository.mode`, which reports writer if any shard's connection is writer.

Tradeoff: reads served in reader mode (today, mostly GraphQL reference lookups) no longer warm the cache. On deployments without a separate reader pool, those reads were actually served by the writer and were safe to cache, so they lose a small caching benefit.

## Testing

- New `repo.test.ts` case: a read in reader mode does not populate the cache, and a later writer read does. Fails without the fix.
- The multi-shard case (writer work on one shard, then a replica read on another) was reviewed but not covered by a test: there is no repo-level test setup with multiple real shards.
- `repo.test.ts`, `fhir/repository/`, `routes.test.ts`, `batch.test.ts`, and `operations/graphql.test.ts` pass.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5b1a8ff293d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.