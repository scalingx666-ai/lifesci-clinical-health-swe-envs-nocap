# Issue

**Title:** fix(stock): apply Company user permissions in Stock Ageing report (backport #65810)

## Description

Backport of #65810 to `version-15-hotfix`. The version-16 backport is #67032.

The Stock Ageing report read Stock Ledger Entries without the user's Company user permissions, so a user restricted to one company could see the available quantity, average age and stock value of each item in another company. The report now leaves out the stock of companies the user is not permitted to see.

**Fix:** The Stock Ledger Entry query in `FIFOSlots` now also filters on the companies that the Company user permissions of the user allow for Stock Ledger Entry. Users without a Company user permission see the same result as before. ()

**Changes compared with develop:** `company_restriction.py` and `get_allowed_companies_condition` do not exist on `version-15-hotfix`. The Stock Ledger Entry query gets the allowed companies with `get_allowed_docs_for_doctype(get_user_permissions().get("Company", []), "Stock Ledger Entry")`, the same pattern as the Warehouse user permission check above it, and adds `sle.company.isin(companies)`. The result is the same as on develop.

 for the example and the steps to test.

### Tests

- `test_company_user_permission_limits_item_rows`: passes on this branch, fails on `version-15-hotfix` without the fix (the restricted user gets the quantity 6).
- `test_permitted_company_user_sees_item_rows`: passes on this branch and without the fix (must-still-work check).
- `test_stock_ageing.py` (complete file): 49 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.