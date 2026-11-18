# Issue

**Title:** fix: Merge Garmin epoch slots split accross pushes

## Description

A Garmin epoch slot whose activity types arrive in separate pushes is now stored as the sum over all of them. Each push records its slot's per-type values in a Redis hash, and the stored value is the sum over the hash. The epoch write uses a new `keep_greater` mode of `bulk_create`, so a lower value never replaces a stored one. Other callers still keep last-write-wins without changing the interface (default is False).

This serves as a . Garmin splits large pushes into requests of 100 epochs that arrive ~1s apart (checked with S3 payloads). A slot that is split loses whichever half lands first, e.g. `WALKING 654 steps` followed by `SEDENTARY 0` is stored as 0 steps in total.

Also for the future - checked docs and added other epoch types (which we don't necessaarily ingest as of now), to prevent this issue from reappearing in the future

why not `GREATEST` alone as suggested in #1913? This would get steps right in most cases observed, but e.g. it would undercount calories which are split into walking, generic etc.

`GREATEST` in this case could also be replaced by a lock, but in my opinion keeping the largest value is a cleaner option, and it would result in the same since we won't keep lower values (e.g. 0 upserting a higher value) and it will eventually converge to the full sum regardless.

## Changes during review

> _Added during review by Sebastian Kalisz._

The Health API says new epochs always replace stored ones with the same start time (§7.2), also after Garmin reconciles two devices into one record that can hold fewer steps (§6.1). `keep_greater` would have kept the higher, stale value in that case, so it is gone, and the repository is unchanged:

- The requests of one push take a transaction lock per slot (`pg_advisory_xact_lock`, sorted keys), held until the push's commit. They write in turn, so the last one stores the full sum and a plain upsert is enough; no request can overwrite a fuller sum with an older one.
- Redis joins a slot's activity types for 15 minutes, the window of one split push, instead of 3 days. A later push of the slot (an epoch completed after a mid-epoch sync, or a reconciled one) starts afresh and replaces the stored value.
- Only the push path joins slots; a pull returns every type of its range at once.

## Breaking change

> _Added during review by Sebastian Kalisz._

None.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Garmin 24/7 activity data now combines activity records received in separate uploads for the same time slot, providing more complete totals for steps and active calories.
  * Pulled activity records remain separate from previously pushed records.
* **Bug Fixes**
  * Concurrent updates for the same user and time slot are handled in sequence to help prevent inconsistent totals.
  * If combining stored records fails, the current upload’s data can still be processed.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27549f81ed48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.