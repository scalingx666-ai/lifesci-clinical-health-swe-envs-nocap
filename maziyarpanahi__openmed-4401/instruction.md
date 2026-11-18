# Issue

**Title:** feat: enforce local audio retention and destruction

## Description

## Description
ASR buffer counters do not own or erase the underlying audio. Add an actual retention owner for bounded mutable buffers, plus explicit cleanup enrollment for completed application-owned files. Finalization, cancellation, expiry and provider failure attempt destruction of every declared artifact; missing or unverifiable artifacts prevent a passing audit.

.

## Type of Change
- [x] New feature
- [x] Documentation update
- [x] Test addition/improvement

## Changes Made
- Bind a complete expected artifact inventory to a non-renewable local policy, opaque session identity and ordered destruction receipts.
- Overwrite owned buffers, invalidate in-flight inference results after cancellation or expiry, sanitize provider exceptions, and enforce byte/operation/lifetime limits. Default timer expiry also covers idle sessions.
- Enroll completed files only in an explicitly supplied private POSIX directory, verify identity and link/permission constraints, quarantine and verify before unlink, preserve unrelated entries and retain failed cleanup for retry.
- Keep external copies and crashed memory unaccounted. Validate bounded host-persisted recovery checkpoints before deletion and preserve lifecycle histories and prior inventory violations across recovery.
- Publish the API, runnable synthetic guide, navigation/publication registration and changelog entry.

No audio or checkpoint is written to disk by this implementation. File enrollment is an explicit cleanup adapter, not permission to record audio. Windows retains the portable buffer implementation and rejects the unsupported file adapter. Receipts establish the stated overwrite/unlink operations within the declared inventory, not physical storage erasure, complete discovery of copies, or compliance certification.

## Testing
- [x] Focused synthetic tests: **57 passed**.
- [x] Full suite: **24,731 passed, 158 skipped, 11,361 subtests passed** (79 warnings; 208.37 seconds).
- [x] `make format`, `make lint`, `make format-check`, `make type-check`, `make brand-check`.
- [x] Explicit mypy on the new module; public API compatibility; classified-effect inventory.
- [x] Strict MkDocs build (149.63 seconds) and runnable guide example.
- [x] Scoped pre-commit, including Bandit and secret detection; `git diff --check`.
- [x] Incoming commit attribution: all seven commits against master and the single feature commit against the prerequisite merge.
- [ ] Hosted checks: pending on this PR's exact head.

Tests inspect real owned-buffer contents and file absence, deadline/clock failure, provider failure, cancellation during inference, incomplete inventories, failed-cleanup retry, replacement/symlink/hardlink and permission changes, unexpected entries, crash recovery and malformed checkpoints. File tests are explicitly POSIX-scoped; portable buffer and unsupported-adapter tests run across platforms.

## Documentation
- [x] Added public API docstrings and `docs/multimodal/streaming/audio-retention.md`.
- [x] Updated changelog, MkDocs navigation and publication inventory.

## Dependencies and Integration
- [x] No new third-party dependencies.
- Contains latest master `29ffa70050cc7729a0051be419a1b090699a5ed1`.
- This branch preserves the prerequisite speaker-alias, transcript-lineage, PHI-withholding and role-review commits from #4386, #4388, #4392 and #4400. Its base remains master so full CI runs.
- Merge those prerequisites first; the issue-specific change is commit `a6fbea0f527de92417e39c2e0c9106b58e386394` (seven files). The cumulative diff includes those still-open prerequisites.

## Example
`capture → buffering → infer → finish` overwrites the owned buffer and emits `owned_buffer_overwritten`. An expected external buffer or an altered enrolled file keeps `passed: false`; recovery cannot erase that earlier inventory violation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `775b655d703c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.