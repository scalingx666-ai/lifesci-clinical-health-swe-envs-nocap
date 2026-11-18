# Issue

**Title:** fix(buying): don't delete an order row that was returned

## Description

**Problem:** Update Items on a Purchase Order deletes a row that was received and then fully returned, since only `received_qty` (net of returns) is checked. The Purchase Receipt and its return still link the deleted row, so a Purchase Invoice made from the receipt fails with "Invalid reference Purchase Order Item". With the default "Bill for rejected quantity in Purchase Invoice" setting, the invoice maps the returned row too (by design, see `test_purchase_receipt_bill_for_rejected_quantity_in_purchase_invoice`).

**Fix:** a row with `returned_qty` cannot be deleted either. The same check is added for Sales Order rows (`delivered_qty` is also net of returns there).

The reporter asked to keep the deletion and let the invoice skip the returned row. This PR blocks the deletion instead, so no submitted document links a missing order row. To re-order the returned qty, a new Purchase Order can still be made.

### Steps to reproduce
1. Submit a Purchase Order with two items and a Purchase Receipt for it.
2. Make a return of the second item and submit it.
3. On the Purchase Order, Update Items and remove the second row.
4. Create > Purchase Invoice from the Purchase Receipt and submit it.

Before: step 3 deletes the row and step 4 fails with "Invalid reference Purchase Order Item". After: step 3 fails with "Cannot delete item ... which has already been received".

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f52cd39ca6a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.