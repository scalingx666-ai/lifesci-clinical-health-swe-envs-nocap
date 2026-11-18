# Issue

**Title:** fix(backend): back off on a throttled request instead of failing the sync

## Description

## What does this change?

A throttled Withings request (envelope status 601) is now retried with the backoff the shared client already uses for HTTP 429, instead of failing the domain it belongs to.



## Why?

The fix suggested in the issue, handling 601 in `withings_request`, would never run: Withings answers HTTP 200 with the status in the envelope next to an `error` message, and the shared client's body check raised a generic 400 on that message before `withings_request` saw the envelope. The unit tests mocked an envelope without `error`, so they passed on a shape the API never sends.

`make_authenticated_request` gains `check_body_errors` (default unchanged), which `withings_request` turns off; it then retries 601 on the shared `MAX_RETRIES` / `RETRY_BASE_DELAY`. Other Withings errors now surface with their Withings status (401, 502) rather than 400.

## How did you test this?

Tests through both layers with the real envelope shape, each failing without its half of the fix. Against the API on a development app: an unknown action returns `{"status": 2554, "error": "Not implemented"}`, which raised a generic 400 before and now reaches `WithingsAPIError`. Parallel requests tripped the throttle at exactly 120; a request made right after waited 15, 30 and 60 s and succeeded on the last attempt, so the window lasts about a minute and the full backoff is what clears it.

## Worth knowing

- Under sustained throttling a Withings sync now holds its worker up to 105 s per request instead of failing fast.
- Retries carry no jitter, like the existing HTTP 429 path, so workers throttled together retry together.

## AI usage

Claude Code for tracing the error path, drafting the fix and tests, and probing the API.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Withings requests now retry temporary throttling responses, with increasing delays between attempts. Successful retries return the response as expected; persistent throttling is reported as an error.
  * Provider responses with body-level errors are now surfaced as errors by default, while integrations that use their own status envelopes can bypass these checks.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9619eeeb80bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.