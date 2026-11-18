# Issue

**Title:** refactor(backend): remove unused Garmin save_* and backfill helpers

## Description

## What does this change?

Removes the Garmin `save_*` methods, `get_body_composition`, the four `trigger_*_backfill` wrappers and `get_max_days_for_type`, as listed in #2010. `save_sleep_data` and `save_activity_data` stay.

## Why?

Since #410 everything goes through `process_items_batch` and the `_build_*` helpers. The old methods looked like a second ingestion path, so a fix could land in one that never runs.

Closes: #2010

I took the removal in one PR as @GrelaM100 suggested on the issue.

## How did you test this?

Nothing changes at runtime: before deleting, I grepped `backend/` and the rest of the repo for each name, and the only callers were tests (`save_hrv_data`, `save_dailies_data`, `save_body_composition`). Nothing references them after the change.

Tests: the `save_hrv_data` tests and the `save_dailies_data` test now call `process_items_batch` with the same assertions. I dropped the two `save_body_composition` tests because `_build_body_comp_samples` already covers the same cases (4 samples, missing timestamp). The one thing I'm unsure about is whether you want those two moved instead of dropped.

```
cd backend
uv run pytest tests/providers/garmin -q     # 131 passed
uv run ruff check / ruff format --check     # clean
```

Full backend suite: 17 tests fail here, and the same 17 fail on unmodified main (my machine is in UTC+5, and at least one failure is a timezone assertion). I did not dig into them. `ty` reports no new diagnostics on the Garmin code.

#1963 edits the same `save_body_composition` tests, so whichever of the two merges second will need a small rebase.

Nothing here touches a provider API, so there was no real-account test.

## AI usage

Claude Code (Sonnet 5.5) located the dead code, made the deletions and drafted the tests. I reviewed the diff and the test migration.

🤖 Generated with [Claude Code](https://claude.com/claude-code)


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Refactor**
  * Garmin data processing and historical sync now use consolidated workflows. Some previous processing and backfill options are no longer available through their former routes.
  * The changes do not indicate a change to Garmin data or historical sync features visible to end users.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4428ef76fc0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.