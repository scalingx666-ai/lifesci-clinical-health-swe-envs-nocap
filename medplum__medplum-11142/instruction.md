# Issue

**Title:** feat(server): add readonlyBatchOnReader project setting

## Description

Adds a `readonlyBatchOnReader` project setting. When it is enabled, a `batch` bundle whose entries are all read-only runs on the reader database pool instead of the writer.

Today, batch entries never use the reader: `searchOnReader`, `chainedSearchOnReader`, and GraphQL all skip reader routing when `options.batch` is set, because a mixed batch may read its own writes. A batch made up entirely of reads and searches has no such concern.

## How it works

`BatchProcessor.preprocessBundle()` already classifies every entry by its routed interaction. It now also records `readOnly`, which is true only when every entry is one of `read`, `vread`, `search-type`, `search-system`, `history-type`, `history-instance`, or `history-system`. In `run()`, a non-transaction batch with `readOnly` set and the setting enabled calls `repo.setMode(RepositoryMode.READER)` before processing entries.

- The classification comes from the router's route match, so a write entry cannot be labeled read-only.
- Any `create`, `update`, `patch`, `delete`, `operation` (including `$graphql`), or nested bundle entry keeps the whole batch on the writer.
- Transactions are unaffected.
- Preprocessing does not query the database for read entries, so no writer connection is open when the mode is set.

## Not included

- Async batches (`Prefer: respond-async`) go through `processNextEntry()` in the batch worker and are not covered yet. `readOnly` is stored in `BundlePreprocessInfo`, so it is persisted with the initial state and can be used there in a follow-up.
- No docs or server-level default.

## Testing

- New `routes.test.ts` case: with the setting enabled, an all-search batch hits only the reader pool, and a batch with a create hits only the writer.
- `fhir-router` tests and the server batch, checkpoint store, and batch worker tests pass.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `baed14789fc1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.