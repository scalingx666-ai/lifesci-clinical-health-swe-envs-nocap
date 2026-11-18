# Issue

**Title:** OBLS-1003 Remove the regression suite's category commit wait

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** https://openboxes.atlassian.net/browse/OBLS-1003

**Description:**

Removes `CategoryCommitFilter` from the regression suite. It was a client-side workaround: after a `POST /api/categories` it polled the database until the new category was committed, because the server could hand back the response before its transaction committed. `DeferResponseCloseFilter` (#6262) fixes that on the server side for every integration spec, so the client-side wait is no longer needed.

Two files, deletions only: the filter class, and its four references in `RegressionApiTrackingExtension`.

**Verification:**

- `DeferResponseCloseFilterSpec` (from #6262) holds a category insert open inside the commit and checks that the client is still waiting. A copy of it, placed in the regression package and run under `regressionIntegrationTest`, passes; with the filter's registration removed from `IntegrationSpecConfig`, it fails ("client completed while the commit was held"). So the regression suite's specs do run with the server-side filter.
- Full `regressionIntegrationTest` with this change: MySQL 8.0.36 and MariaDB 10.3.39, 1245 tests, 0 failures each.

### :camera: Screenshots & Recordings (optional)

N/A, test code only.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a54926166f51`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.