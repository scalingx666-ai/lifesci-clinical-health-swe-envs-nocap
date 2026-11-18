# Issue

**Title:** test(backend): block network access and ignore local .env in tests

## Description

## What does this change?

Backend tests no longer load `config/.env` and fail if they open a TCP connection to anything other than loopback or the test Postgres/Redis. The six disconnect tests that were calling Garmin and Polar now mock the deregistration call.

## Why?

Disconnect tests have been calling Garmin's and Polar's real deregistration endpoints with fake tokens since deregistration was added - they passed only because the 401 is caught and logged. Nothing in the test setup stopped that, so it went unnoticed.

Tests also read the developer's `config/.env`, so local results depended on whoever's config was there: with mine, 11 tests failed that pass on CI (telemetry and scores flags), and Ultrahuman/Garmin webhook tests kept trying to reach my local MinIO, which made the suite several times slower. It's easy to point `.env` at a real S3 bucket for some manual testing and forget about it - then the tests would quietly write to that bucket.

The guard records blocked connections and fails the test at teardown, because the code under test often swallows the exception (that's exactly how the disconnect tests hid it). `SECRET_KEY`/`MASTER_KEY` moved to `tests/__init__.py` - in `conftest.py` they were set after `app.config` was imported, so they never took effect.

## How did you test this?

Full suite locally, with my own `config/.env` in place:

| | main | this branch |
|---|---|---|
| Result | 11 failed, 3014 passed | 3026 passed |
| Tests reaching provider APIs | 6 (`apis.garmin.com`, `www.polaraccesslink.com`) | 0 |
| Duration | 9:32 | 2:39 |

Before mocking deregistration, the guard flagged exactly those six tests, e.g. `Failed: Test tried to reach the network: apis.garmin.com:443`.

## AI usage

Claude Code (Opus 5.5) for finding which tests hit the network and drafting the fixtures.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Configuration**
  * Setting `OW_IGNORE_ENV_FILE` to a nonempty value prevents application settings from loading values from a local environment file. When unset or empty, the existing settings behavior remains unchanged.
* **Tests**
  * Automated tests use fixed defaults for key settings and restrict TCP connections to loopback and the configured test database and cache services. Tests fail if they attempt other TCP connections, including when the connection error is caught.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32f0735d526b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.