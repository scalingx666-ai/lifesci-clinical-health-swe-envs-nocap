# Issue

**Title:** fix(stock): apply Company user permissions in Warehouse Wise Stock Balance report (backport #65798)

## Description

Backport of #65798 to `version-15-hotfix`. The version-16 backport is #67028.

The Warehouse Wise Stock Balance report read warehouses without the user's Company user permissions, so a user restricted to one company could see the warehouse tree and the stock value of each warehouse of another company. The report now lists only warehouses of the companies the user is permitted to see.

**Fix:** The Warehouse query in `get_warehouses` now also filters on the companies that the Company user permissions of the user allow for Warehouse. Users without a Company user permission see the same result as before. ()

**Changes compared with develop:** `company_restriction.py` and `get_allowed_companies_condition` do not exist on `version-15-hotfix`. The report gets the allowed companies with `get_allowed_docs_for_doctype(get_user_permissions().get("Company", []), "Warehouse")`, the same pattern that Stock Ageing and Stock Analytics already use for Warehouse user permissions, and adds `["company", "in", companies]` to the Warehouse filters. The result is the same as on develop. Users without a Company user permission get no extra filter. The test file uses `FrappeTestCase`; the conflict with `test_empty_disabled_group_stays_above_its_enabled_children` was resolved by keeping both tests.

 for the example and the steps to test.

### Tests

- `test_company_user_permission_limits_warehouses`: passes on this branch, fails on `version-15-hotfix` without the fix (the restricted user gets the `_Test Company` warehouses).
- `test_warehouse_wise_stock_balance.py` (complete file): 5 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.