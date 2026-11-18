# Issue

**Title:** refactor(server): repair NULL HumanName.projectId in bounded batches

## Description

, addressing  reuse v49's bounded batching for the v50 repair.

- Moves v49's `runBatch` (READ COMMITTED + serialization-failure retry) into a new `migrations/data/utils.ts` as `runReadCommittedBatch`, generic over its summary row. v49 and v50 both use it, and v50 keeps its own batching defaults (5000 rows, 100ms between batches).
- `repairNullHumanNameProjectIds` now runs one statement per batch. Each statement takes up to `batchSize` NULL rows, sets `projectId` from the owning resource (falling back to the system project), and deletes rows that have no owner. The loop stops when a batch finds no NULL rows.
- Re-selecting `projectId IS NULL` always makes progress because each batch fixes or deletes every row it picks up. v49's `("projectId", ...)` btree indexes serve the `IS NULL` lookup, so batches don't rescan the table. I checked this with `EXPLAIN`.
- The two migration results (update, delete) are now one: `Repair NULL HumanName.projectId` with `updated` and `deleted`.

**Testing:** `v50.test.ts` passes. The repair test now uses `batchSize: 1`, so the patient's two names are handled in separate batches.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `461ce9f2dd82`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.