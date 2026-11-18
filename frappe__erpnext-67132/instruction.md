# Issue

**Title:** fix(stock): keep the Item select check and apply Stock Entry scoped warehouse permissions in get_warehouse_details

## Description

. `get_warehouse_details` gives the stock quantity and the valuation rate of an item in a warehouse to the Stock Entry form. #65912 replaced its Item select check with a Stock Entry read check, and checked the warehouse twice: once as a Warehouse document and once for Stock Entry. Now the Item select check is back next to the Stock Entry check, and the warehouse is checked once, with the User Permissions that apply to Stock Entry.

**Example:**
- **Setup:**
   - User A has only a custom role that has read permission on Stock Entry and no permission on Item.
   - User B has the Stock User role, a User Permission with **Allow** Warehouse and **For Value** `Stores - TC` for all document types, and a second User Permission with **Allow** Warehouse, **For Value** `Finished Goods - TC` and **Applicable For** Stock Entry.
- **Steps:**
   1. As user A, call `erpnext.stock.doctype.stock_entry.stock_entry.get_warehouse_details` with item `Steel Sheet` and warehouse `Stores - TC`.
   2. As user B, open a new Stock Entry and add a row for `Steel Sheet` with **Target Warehouse** `Finished Goods - TC`.
- **Before the fix:** user A got the quantity on hand and the valuation rate. User B got a permission error, although the Stock Entry form lets user B select `Finished Goods - TC`.
- **After the fix:** user A gets a permission error. User B gets the **Basic Rate** and **Actual Qty (at source/target)** of `Finished Goods - TC`, and still gets a permission error for a warehouse that is not in the User Permissions.

**Fix:** `get_warehouse_details` checks Item select permission again. `check_stock_entry_warehouse_permission` checks the warehouse and the company of the warehouse against the User Permissions that apply to Stock Entry, in place of `erpnext.require_user_permission("Warehouse", ...)`. ()

**Note for reviewers:**
- Desk users get Item select through the Desk User role, so the Item check only refuses users without desk access or with custom roles. It is the check that was there before #65912.
- The company check keeps what `require_user_permission` did for the company of the warehouse: a user limited to one company still gets a permission error for a warehouse of another company (`test_get_warehouse_details_applies_company_user_permission`).
- The same change is in the backports #67013 (`version-16-hotfix`) and #67054 (`version-15-hotfix`).

### How to test

1. Create a role without desk access that has read permission on Stock Entry only, and a user with only that role. As that user, call `get_warehouse_details` for an item and a warehouse. You get a permission error.
2. Give a Stock User a User Permission on Warehouse `Stores - TC` for all document types, and one on `Finished Goods - TC` with **Applicable For** Stock Entry.
3. As that user, call `get_warehouse_details` for `Finished Goods - TC`. You get the quantity and rate.
4. Call it for a third warehouse. You get a permission error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b112a5f8dfa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.