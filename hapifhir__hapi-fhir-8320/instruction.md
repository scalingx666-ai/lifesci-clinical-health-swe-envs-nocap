# Issue

**Title:** GL-9258: Reindex v3 fails permanently on retryable TRM_VALUESET lock conflict

## Description

### For Code Reviewer

`RetryChunkLaterException` thrown by a bulk-modify step's pre-flight guard (`processPidsOutsideTransaction`) was being caught by the generic `catch (Throwable)` in `BaseBulkModifyResourcesStep.processPids` and converted into a permanent per-resource failure instead of deferring the chunk. That is what made Reindex v3 fail with `HAPI-2790` instead of retrying when a concurrent `ValueSet` pre-expansion holds the same `TRM_VALUESET` rows.

Approach, per review feedback: rather than special-casing `RetryChunkLaterException`, the exceptions that tell the batch2 framework how to handle a chunk or job (`RetryChunkLaterException`, `JobExecutionFailedException`, `ReductionStepFailureException`) now share a marker interface, `IBatch2FrameworkException`. The bulk-modify catch-all rethrows anything implementing it, so future framework signals are not swallowed either. The batch2 docs (`server_jpa_batch/introduction.md`) gain an "Exceptions Thrown by Job Steps" subsection stating the rule for step authors.

Areas worth a closer look:

- **Pre-flight hoisted above the `try`.** `processPidsOutsideTransaction` now runs before the `try`, so *generic* (non-retry) exceptions from it also propagate out of `run()`. `StepExecutor` then marks the chunk a retriable `ERRORED` chunk (capped at 3 attempts, then `FAILED`) instead of attributing a chunk-level guard failure to every resource in the chunk. This is deliberate; per-resource attribution was misleading for a chunk-level guard.
- **`StepExecutor` change.** It now also catches `ReductionStepFailureException` alongside `JobExecutionFailedException` and fails the chunk immediately (`onWorkChunkFailed`), with no retry. Previously a `ReductionStepFailureException` thrown from a work-chunk step fell into the generic path and became a retriable `ERRORED` chunk. This is needed because the bulk-modify step now propagates it rather than recording it per resource, and retrying an unrecoverable exception is wrong. It affects every job's work-chunk steps, not only bulk-modify.
- **Deferral restarts the chunk.** A deferred chunk re-runs from the beginning, so PIDs already committed earlier in the chunk are reprocessed. This is documented in the javadoc on `processPidsOutsideTransaction` and `processPidsInTransaction`.

Tests: parameterized `BaseBulkModifyResourcesStepTest` (unit, covers each framework exception from both hooks, plus the generic-exception behaviour); a `WorkChunkProcessorTest` case for `ReductionStepFailureException`; and a real-stack `ReindexV3ModifyResourcesStepTest` case that drives the actual `HAPI-2830` guard through the Reindex v3 step.

### For QA

- [ ] A `$reindex` (Reindex v3) job whose pre-flight guard throws `RetryChunkLaterException` (for example a `CodeSystem` with pending terminology storage, `HAPI-2830`, or a concurrent `ValueSet` pre-expansion holding `TRM_VALUESET` rows) now defers the affected chunk (`POLL_WAITING`, then retried) instead of the job ending `FAILED` with `HAPI-2790`. Once the condition clears, the job completes successfully.
- [ ] A generic (non-retry) exception from the pre-flight guard now fails the whole chunk as a retriable `ERRORED` chunk (capped at 3 attempts) rather than marking every resource in the chunk as individually failed. Confirm this is the intended, reviewed behaviour change, not a regression.
- [ ] A work-chunk step that throws `ReductionStepFailureException` now fails its chunk immediately (`FAILED`, no retry) instead of `ERRORED` and retried. Other jobs' failure handling (`JobExecutionFailedException` still fails immediately; generic exceptions still go `ERRORED` and retry) is unchanged.
- [ ] Normal bulk-modify and `$reindex` runs with no guard conflict still complete, and per-resource failures inside the transaction are still reported against the individual resources.
- [ ] Docs: the new "Exceptions Thrown by Job Steps" subsection in the batch2 introduction page renders correctly and reads accurately.
- [ ] Support/QA note: unlike the generic-exception path, a chunk deferred via `RetryChunkLaterException` has no attempt cap. It cycles `POLL_WAITING` to `READY` for as long as the guard condition holds true. If that condition became permanently true, `$reindex` would poll roughly every 30 seconds indefinitely with no error surfaced, instead of failing fast with `HAPI-2790`. So the visible symptom of a stuck reindex changes from "job `FAILED` with `HAPI-2790`" to "job stuck in progress in `POLL_WAITING`, no error surfaced". When investigating a reindex that appears hung, check job status and how long it has been `POLL_WAITING`, not just jobs that ended `FAILED`. This is the existing, long-standing batch2 `POLL_WAITING` contract (Reindex v2 has behaved this way for years), not new behaviour introduced by this fix.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `510a505c6f49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.