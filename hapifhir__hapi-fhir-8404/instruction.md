# Issue

**Title:** [8387] STORAGE_PARTITION_SELECTED is not invoked for partition-selecting operations without a resource type

## Description

## Problem

`STORAGE_PARTITION_SELECTED` was only fired when the request carried a resource type. Partition-selecting requests without one — system-level `_history`, result paging, transactions, server-level operations — skipped the hook entirely, so a client scoped to one partition could read another partition's data.

## Change

`BaseRequestPartitionHelperSvc.validateAndNormalizePartition()` now fires the pointcut for every partition-selecting resolution. When no resource type applies, the `RuntimeResourceDefinition` hook parameter is `null`, which its Javadoc already allows.

## Upgrade note

Interceptors hooking `STORAGE_PARTITION_SELECTED` must handle a `null` `RuntimeResourceDefinition`.

## Tests

- `RequestPartitionHelperSvcTest` — hook fires with a null resource definition for system history, server operations, page fetches, and generic (transaction) resolution.
- `PartitioningSqlR4Test` — system-level history fires the hook, and an interceptor that throws blocks the query before it runs.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbc41d67cafc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.