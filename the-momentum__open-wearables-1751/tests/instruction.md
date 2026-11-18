# Issue

**Title:** fix(backend): persist Samsung sleep score sent by the SDK

## Description

## What does this change?

Samsung sleep sessions from the SDK now come with a `sleep` health score. The SDK already sent Samsung's `SLEEP_SCORE` as a `sleepScore` value on every sleep entry, but the backend ignored `values`, so the score was dropped. The score is now kept in the Redis sleep state and saved when the session is finalized, as a `HealthScore` (provider `samsung`, category `sleep`) linked to the session. Samsung's coverage now declares `HEALTH_SCORES = {sleep}`, and `coverage.mdx` is regenerated.

## Why?

[`SleepType.SLEEP_SCORE`](https://developer.samsung.com/health/data/api-reference/-shd/com.samsung.android.sdk.health.data.request/-data-type/-sleep-type/index.html) is a documented, read-only `Field<Int>` in the Samsung Health Data SDK, and `SamsungHealthManager.convertSleep` already forwards it. This is the only provider sleep score we get from Samsung, and users lost it.

The change is in the shared SDK sleep service and is keyed on the `sleepScore` value type, not on the provider. Apple and Health Connect don't send this value, so nothing changes for them.

Choices:
- `recorded_at` is the session start, the same as Polar. The internal OW score keeps its own anchor (local wake time) and is untouched.
- The Samsung range is set to `0-100` in `HEALTH_SCORE_RANGES`. Samsung doesn't document the range.
- When a session is merged with an adjacent DB record, the old record and its score are deleted (cascade) and the new state's score is saved. That works for Samsung because every sleep entry carries the score.

Related issue: #1723

## How did you test this?

Automated tests only: new unit tests plus one end-to-end test on Postgres and Redis for the Samsung sleep score in `tests/services/test_sleep_service.py`. Not tested against a real Galaxy Watch sync.

## AI usage

Claude Code: checked the Samsung SDK docs, traced the SDK and backend code, wrote the change and tests, drafted this description.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Samsung sleep scores are now captured and saved alongside sleep sessions on a 0–100 scale.
* **Documentation**
  * Updated health score coverage information to show Samsung sleep score support.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b03587b3ffb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.