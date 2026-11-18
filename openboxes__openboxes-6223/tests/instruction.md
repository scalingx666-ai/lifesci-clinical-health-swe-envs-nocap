# Issue

**Title:** Make cycle count views work with ONLY_FULL_GROUP_BY

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**

**Description:**
On MySQL 8, where ONLY_FULL_GROUP_BY is on by default, the cycle count candidates and pending requests endpoints return a 500 because `cycle_count_session` and `pending_cycle_count_request` select columns that are neither grouped nor aggregated. This drops the unused `abc_class` from the `cycle_count_metadata` subquery and takes the remaining columns with `MAX()` and `MIN()`. On seeded data both views return the same rows as before on MySQL 8 and MariaDB. The new API spec covers both endpoints and fails on MySQL 8 without the fix.

MariaDB 10.3 with ONLY_FULL_GROUP_BY turned on still can't run the migrations, because it rejects the `product_demand` view when it's created. That's outside the cycle count views, so I left it out.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e6e729aaeb4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.