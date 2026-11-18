# Issue

**Title:** Stop in-flight batch2 work before JPA test cleanup purges the database

## Description

Part of #8436

The changes made here prevent batch2 leftover-work interference within a Spring test context. The more frequent cause for intermittence is reusing the same in-memory database within the same Spring test context. See: #8464

JPA test cleanup purged the database while batch2 work from the finished test was still running. Cancelling a job only sets a flag, so a `ValueSet` pre-expansion could keep writing, and keep caching resource IDs for rows the purge had deleted, into the next test. The after-test running-jobs check never caught it: `hasRunningJobs()` read page 1, so  it missed every job.

### Changes
- `BaseJpaTest.runWithSchedulersPausedAndBatch2Stopped`: pauses the schedulers, cancels all jobs and waits for in-flight batch2 work, then runs the cleanup. The R4 and R5 base classes purge through it. If the wait times out, the purge still runs and the test fails afterwards, so the next test starts clean.
- `Batch2JobHelper.awaitNoInFlightWork()`: new. Waits until no work chunk is queued or running and the reducer is idle, for 50 ms in a row; on timeout, names what is still running. Its dependencies come through a new constructor that `TestJPAConfig` uses. The existing constructor is unchanged.
- `Batch2JobHelper.hasRunningJobs()` and `cancelAllJobsAndAwaitCancellation()`: read every page of unfinished jobs through `IJobPersistence`.
- `BaseJpaR4Test.afterCleanupDao`: jobs still running at the end of a test log a warning instead of failing, since cleanup now stops them safely.
- `ReductionStepExecutorServiceImpl.isIdleForUnitTest()`: test-only accessor for the reducer's state.
- `Batch2JobHelper.cancelAllJobsAndAwaitCancellation` was marked as deprecated in favour of `Batch2JobHelper.cancelAllJobs` because waiting cancellation was not actually true and they cannot be done like so in one method.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f5e1e5af645`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.