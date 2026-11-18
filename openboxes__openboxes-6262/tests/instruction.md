# Issue

**Title:** OBLS-1003 Fix flaky API specs racing transactional controller commits

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-1003 (backport of #6183 from develop)

**Description:**

Brings #6183, merged into `develop` on 2026-10-01, to this branch unchanged (cherry-pick of 4b6ab285d; three files
under `src/integration-test`, nothing packaged into the WAR).

The existing API specs on this branch fail intermittently in the "Test Pull Request" backend job: a spec creates a
record, then uses it, and the second request can arrive before the first request's transaction has committed. On
#6258 and #6260 the job failed this way in `ProductApiCRUDSpec`, `LocationGroupApiSpec`, `LocalizationApiSpec` and
`ProductClassificationApiListFiltersOutEmptySpec` (for example a foreign key error on the category the spec had just
created); the re-runs passed. #6183 describes the cause and the test-only filter that fixes it.

## Verification (local, JDK 8)

On this branch with MySQL 8.0.36: `integrationTest` 69 tests, 0 failed, 2 skipped (includes the
`DeferResponseCloseFilterSpec` from #6183); `regressionIntegrationTest` 1245 tests, 0 failed, 272 skipped.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c1cb7302505`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.