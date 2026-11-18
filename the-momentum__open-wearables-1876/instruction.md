# Issue

**Title:** fix: One Redis state per writer app for Apple Health sleep sessions

## Description

This change makes it so that open SDK sleep sessions in Redis are now kept one per writer app rather than one per user, so a 3rd party write gets its own sleep record instead of being merged into another session.

Before: `sleep:active:{user_id}` -> one `SleepState`, every sample from every app lands in it.
After: `sleep:sessions:{user_id}` hash, one field per `{provider}:{writer}` -> one `SleepState` each.

Why?
All sleep samples from all sources went into a single session whose source was decied by which sample came first, so multiple provider's sleeps were merged into one ()

For ongoing sessions - the old key is copied into the hash on first run of `finalize_stale_sleep` task or first sleep upload after deploy, so the change is backwards compatible and wont break ongoing sessions.

This change can't cover already stored and merged sleeps, they would need to be deleted and re-synced, however we just can't force SDK to re-send sleep samples, so leaving it be.

From what we discussed, it is highly likely that we can send one full sleep session from Apple SDK rather than each stage by itself - which would remove the need to even keep the state in Redis, but before that it will still work wrong and it's not easy to tell when that change could be deployed.

This is mostly made possible by merging #1781, which adds source app id to state.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Sleep sessions from different providers and source apps are tracked separately, keeping overlapping sleep data and stages associated with the correct source. Apple Health sources continue to be grouped as one writer.
* **Bug Fixes**
  * Stale sleep sessions are finalized independently, so one session no longer prevents other eligible sessions from being completed.
  * Sleep scores are assigned to the matching session, and adjacent sleep records are matched using their source app when available.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e204440e79c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.