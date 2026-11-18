# Issue

**Title:** OBLS-1015 Port develop's upload and URL handling to the branch

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-1015 (follow-up to OBLS-767)

**Description:**

Brings develop's #5944 (upload and URL handling) to this branch. The OBLS-767 merge took develop as of 8 June; #5944 reached develop with the 0.9.8 release on 12 June, so the branch does not have it yet.

This is `git cherry-pick -x a599007325` (the #5944 squash commit) onto the current branch tip. It applied without conflicts and without hand edits; authorship is kept. It includes upstream's specs from #5944 (`DocumentSpec`, `ReportControllerDownloadShippingReportSpec`).

## Verification

Run locally the way this branch's workflows run it (backend, regression and frontend workflows), on the branch as of #6259 (the branch has since gained #6258, which changes only the regression workflow and its docs; this PR is rebased on it):

- Backend (`./gradlew jacocoTestReport`) on `TEST_DATABASE=mysql:8.0.36` and on `mariadb:10.3.39`: unit 1,177 tests, integration 69 tests, 0 failed on both. The two new specs: `DocumentSpec` 14/14, `ReportControllerDownloadShippingReportSpec` 13/13.
- Regression suite (`./gradlew regressionTest regressionIntegrationTest`) on both databases: 2,433 unit and 1,245 integration tests, 0 failed (67 and 272 skipped are the suite's pending features).
- Frontend (`npm ci && npm test`, then `npm run bundle`, Node 14): 244 suites, 2,405 tests: 2,329 passed, 76 skipped, 0 failed; the bundle builds. This change touches no frontend file.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a54926166f51`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.