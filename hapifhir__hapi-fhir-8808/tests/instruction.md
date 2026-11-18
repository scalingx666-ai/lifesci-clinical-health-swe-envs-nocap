# Issue

**Title:** Processing a redelivered work chunk sleeps holding a row lock while waiting for initial work chunk processing to complete

## Description

## The Problem

Since 8.10.0 (#7765), a redelivered work notification for a chunk that another worker is still processing slept for
the full ack timeout inside the dequeue transaction, holding the chunk's row lock. The first worker's heartbeat and
completion updates then waited on that lock causing jobs to stall.

## What was done
- move the wait out of the transaction: `handlePotentiallySlowWorkChunk` no longer sleeps. It throws `DelayChunkException` (`HAPI-2887`) inside  `executeInTxRollbackWhenEmpty`. `HapiTransactionService` does not retry `DelayChunkException`. Instead, it rolls back which releases the row lock and rethrows the exception;
- `handleWorkChannelMessage` catches the exception outside the transaction, waits (sleeps), and rethrows it which triggers the retry mechanism;
- The wait(sleep) is now a third of the ack timeout instead of the full ack timeout. A full-length wait makes the waiting consumer miss its own broker deadline causing the broker to consider it failed and redeliver its messages to another consumer. A third of the ack timeout allows the retry mechanism to run within the ack timeout: two retries fit before it expires. When the first worker completes the chunk in that time, a retry discards the message and the consumer meets its deadline.

## For QA

`WorkChannelMessageListenerTest` covers the transaction not being held during the wait, and the wait of a third of the
ack timeout. `Batch2CoordinatorIT` covers a redelivery that arrives while the first
worker is still running: the first worker now completes the chunk and the job completes.

Acceptance criteria the tests can't reach:
- With an external message broker and a PostgreSQL database, run a batch2 job whose step takes longer than the
  broker's ack timeout. The job completes, and the redelivered consumer logs the `HAPI-2887` warning instead of  stalling the job.
- While that redelivery is waiting, the database shows no lock wait on the chunk's `BT2_WORK_CHUNK` row.

🤖 Partially Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a87991a06612`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.