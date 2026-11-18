# Issue

**Title:** fix(stock): check Stock Entry read and warehouse access in get_warehouse_details (backport #65912)

## Description

Backport of #65912 to `version-15-hotfix`. The version-16 backport is #67013.

`get_warehouse_details` gives the stock quantity and the valuation rate of an item in a warehouse to the Stock Entry form. It only checked that the user can select an Item. It now also needs read permission on Stock Entry and access to the warehouse, also when the Warehouse User Permission applies only to Stock Entry.

**Fix:** `get_warehouse_details` checks Stock Entry read permission and the Warehouse User Permission, including a permission with **Applicable For** Stock Entry. ()

**Fix (follow-up):** `get_warehouse_details` keeps the Item select check that this branch had, next to the Stock Entry read check. `check_stock_entry_warehouse_permission` checks the warehouse and its company with the User Permissions that apply to Stock Entry, in place of `erpnext.require_user_permission("Warehouse", ...)`, so a Warehouse User Permission with **Applicable For** Stock Entry is combined with the ones for all document types. ()

**Changes compared with develop:** The cherry-pick conflicts because `stock_entry.py` on develop has a different structure. The change is ported by hand to `get_warehouse_details` on this branch. The develop function also calls `check_warehouse_company` and `check_company` from an earlier develop change that is not on this branch; this PR does not add them. The two develop commits are one commit here. The tests are in `TestStockEntry`, because this branch has no `TestStockEntryCoverage` class. The develop PR had the same two gaps; the same follow-up change is in #67132 for `develop`. Other PRs to `version-15-hotfix` that change `stock_entry.py` and `test_stock_entry.py`: #67075, #67091, #67092. They touch different lines, and each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_get_warehouse_details_needs_stock_entry_read`, `test_get_warehouse_details_applies_warehouse_user_permission`, `test_get_warehouse_details_applies_warehouse_user_permission_for_stock_entry`: pass on this branch, fail on `version-15-hotfix` without the fix.
- `test_get_warehouse_details_needs_item_select` and `test_get_warehouse_details_combines_warehouse_user_permissions_for_stock_entry`: pass on this branch, fail on this branch without the follow-up commit. `test_get_warehouse_details_applies_company_user_permission` (a user limited to one company gets a permission error for a warehouse of another company): passes with and without the follow-up commit.
- `test_stock_entry.py` (complete file): 135 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.