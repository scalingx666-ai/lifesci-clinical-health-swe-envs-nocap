# Issue

**Title:** fix(manufacturing): apply Sales Order user permissions in Production Plan sales order search (backport #65865)

## Description

Backport of #65865 to `version-15-hotfix`. The version-16 backport is #67078.

The Sales Order search on the Production Plan form (`sales_order_query`) listed open Sales Orders without looking at the user's User Permissions. It now applies the user's Sales Order User Permissions (for example on Company or Customer, and on values in the order rows such as Item), the same way `get_so_details` already does.

**Fix:** `sales_order_query` adds the Sales Order user permission conditions, including the link fields of the order rows, from the new `get_user_permission_conditions_qb` in `erpnext/utilities/query.py`. ()

**Changes compared with develop:** This branch has no `production_plan/mapper.py` and no `erpnext/utilities/query.py`, and version 15 Frappe has no `Engine.get_user_permission_conditions`. The change is made in `sales_order_query` in `production_plan.py`. The new `erpnext/utilities/query.py` builds the Sales Order condition itself: the rule that develop uses for the order rows is also applied to the Sales Order name and the Sales Order link fields. The tests import `sales_order_query` and `get_so_details` from `production_plan.py`. The two develop commits are one commit here. #67101 and #67104 also change `production_plan.py` and `test_production_plan.py` in other places. Each merges on its own.

 for the example and the steps to test.

### Tests

- `test_sales_order_query_follows_company_user_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_sales_order_query_follows_item_user_permission_on_order_rows`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_sales_order_query_without_user_permission_lists_all_open_orders` (must still work): passes on this branch and on `version-15-hotfix` without the fix.
- `test_production_plan.py` (complete file): 115 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.