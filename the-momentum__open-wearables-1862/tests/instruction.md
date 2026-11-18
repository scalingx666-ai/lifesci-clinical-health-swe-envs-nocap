# Issue

**Title:** fix: Cap backfill at `max_historical_days` and change arbitrary 365 day limit

## Description

> `POST /api/v1/providers/{provider}/users/{user_id}/sync/historical` takes a days param, limited to 1-365 (`sync_data.py:341-343`). We already have `ProviderCapabilities.max_historical_days`, but this endpoint never reads it. The base implementation just does now - days and starts the task (`base_strategy.py:197-198`).

- cap historical sync at max historical days set in config (if set)
- change arbitrary limit from 365 days to 3650 (10 years) - the rationale was that someone could possibly ask for longer than 1 year, but removing the limit entirely could allow users to fetch data from however long, and requests would multiply and take a long time to return no data. 3650 felt like a balance between freedom and not allowing stupid things to happen
- Garmin uses config value insead of hard-coded 30 days - SSOT

From my research, it seems that only Garmin and Polar (365 days) set a limit on historical backfill (also I believe Health Connect, but that is managed by SDK), the rest only need paging and set a per-request limit so the rest is kept unchanged.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Historical sync requests can specify up to 3,650 days, subject to each provider’s maximum range. Polar requests are capped at 365 days, and Garmin backfills use the provider’s configured limit.
  * Responses report the scheduled window, including its day count and date range.
* **Documentation**
  * Clarified historical-data limits and availability by provider, including data-type-specific ranges for Polar and permission-based limits for Google Health Connect. The requested window defaults to 90 days.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `96e59d47aa57`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.