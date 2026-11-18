# Issue

**Title:** fix(selling): don't delete a bundle row whose packed item is on a purchase order

## Description

**Problem:** Update Items on a Sales Order deletes a Product Bundle row even when a Purchase Order was made for its bundle items. Those Purchase Order rows link the Sales Order's Packed Item (`sales_order_packed_item`), not its row, and the bundle row's `ordered_qty` stays 0, so no check stops it. The Purchase Order then links a Packed Item that no longer exists.

**Fix:** refuse to delete a bundle row when a draft or submitted Purchase Order row links one of its packed items.

#67156 adds the same check for rows linked through `sales_order_item`; the two touch the same call list in `validate_and_delete_children`.

### Steps to reproduce
1. Make a Product Bundle for a non-stock item with one stock component.
2. Submit a Sales Order with the bundle item and any other item.
3. Make a Purchase Order from the Sales Order for the bundle row (draft or submitted).
4. On the Sales Order, Update Items and remove the bundle row.

Before: the row and its Packed Item are deleted. After: "Cannot delete item ... which is already ordered on Purchase Order ...".

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e08476bb7b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.