# Issue

**Title:** fix(stock): apply Company user permissions in Stock Analytics report (backport #65833)

## Description

Backport of #65833 to `version-15-hotfix`. The version-16 backport is #67033.

The Stock Analytics report read Stock Ledger Entries without the user's Company user permissions, so a user restricted to one company could see the stock quantity and value of each item, period by period, in another company. The report now leaves out the stock of companies the user is not permitted to see.

**Fix:** The Stock Ledger Entry query in `apply_conditions` now also filters on the companies that the Company user permissions of the user allow for Stock Ledger Entry. Users without a Company user permission see the same result as before. ()

**Changes compared with develop:** `company_restriction.py` and `get_allowed_companies_condition` do not exist on `version-15-hotfix`, so the import from the develop commit is left out. The Stock Ledger Entry query gets the allowed companies with `get_allowed_docs_for_doctype(get_user_permissions().get("Company", []), "Stock Ledger Entry")`, the same pattern as the Warehouse user permission check above it, and adds `sle.company.isin(companies)`. The result is the same as on develop.

 for the example and the steps to test.

### Tests

- `test_company_user_permission_limits_rows`: passes on this branch, fails on `version-15-hotfix` without the fix (the restricted user gets 10 in August).
- `test_permitted_company_user_sees_rows`: passes on this branch and without the fix (must-still-work check).
- `test_stock_analytics.py` (complete file): 14 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.