# Issue

**Title:** fix(stock): keep company-restricted users to their companies in the Pick List query of Delivery Note (backport #66037)

## Description

Backport of #66037 to `version-15-hotfix`. The version-16 backport is #67036.

`get_pick_list_query` lists the open Pick Lists of a customer in **Get Items From > Pick List** on Delivery Note. It filtered only by the Company and Customer in the filters, so a user restricted to one company could list the Pick Lists and Sales Orders of another company. Now it refuses a Company that the Company user permissions of the user do not allow.

**Fix:** Call the new `check_pick_list_company` with the Company from the filters in `get_pick_list_query`. () The follow-up commit refuses a Company that is not text (for example a number) in `check_pick_list_company` with a validation error, so the Company filter is always compared as text. ()

**Changes compared with develop:** `check_pick_list_company` and `company_restriction.py` do not exist on `version-15-hotfix`. On develop the helper also guards `get_pending_work_orders` and `get_item_details`, which are not part of #66037. This PR adds the helper (without its docstring) and calls it only in `get_pick_list_query`. It gets the allowed companies with `get_allowed_docs_for_doctype(get_user_permissions().get("Company", []), "Pick List")`, which gives the same result as `get_allowed_companies` on develop. The follow-up commit is not part of #66037; the same change for develop is #67097.

 for the example and the steps to test.

### Tests

- `test_pick_list_query_keeps_company_restricted_user_in_own_company`: passes on this branch, fails on `version-15-hotfix` without the fix (no permission error for the user restricted to `_Test Company 1`).
- `test_pick_list_query_refuses_a_company_that_is_not_text`: passes on this branch, fails without the follow-up commit (no error for the Company `123`).
- `test_pick_list.py` (complete file): 105 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.