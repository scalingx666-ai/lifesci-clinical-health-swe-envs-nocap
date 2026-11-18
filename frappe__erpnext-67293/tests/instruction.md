# Issue

**Title:** fix(stock): let a Stock Manager get Landed Cost Voucher items from a Purchase Invoice (backport #67292)

## Description

Issue: #67246. Backport of #67292 to `version-16-hotfix`.

#67034 made **Get Items** on a Landed Cost Voucher check **read** permission on each receipt document. The Stock Manager role, the only standard role that can create a Landed Cost Voucher, has only **Select** permission on Purchase Invoice. So a Stock Manager could pick a Purchase Invoice in **Vouchers**, but could not get its items or save the voucher. The same check also refused the supplier, date and total that the form fetches when a **Receipt Document** is set.

**Example:**
- **Setup:** a user with only the roles **Stock Manager** and **Stock User**. A submitted Purchase Invoice for `_Test Company` with **Update Stock** checked, 2 of a stock item at 100.
- **Steps:**
   1. As that user, create a Landed Cost Voucher for `_Test Company`.
   2. In **Vouchers**, set **Receipt Document Type** to `Purchase Invoice` and **Receipt Document** to the invoice.
   3. Click **Get Items**.
- **Before the fix:** "No permission for Purchase Invoice". Saving the voucher fails with the same message.
- **After the fix:** **Receipt Items** has the invoice row (2 of the item), as before #67034.

**Fix:** `check_receipt_document_access` now checks **select** permission instead of **read**. In Frappe, select permission on a document is also given by read permission, and it still applies User Permissions. A user restricted to another company, or a user with no permission on Purchase Invoice, is still refused. ()

**Changes compared with develop:** None. The commit applies without changes. As on develop, `test_receipt_reads_need_document_access` now expects a Stock User (no permission on Purchase Invoice) to be refused the receipt details, and a Stock Manager to get them. `get_vendor_invoice_amount` keeps its read check.

### Tests

- `test_stock_manager_gets_items_from_purchase_invoice`: a Stock Manager gets the items from a Purchase Invoice. A Stock Manager restricted to `_Test Company 1` and a Stock User are still refused. Fails on `version-16-hotfix` without the fix, passes with it.
- `test_landed_cost_voucher.py` (complete file): 44 tests pass.
- Differential run on v16bp4.localhost against `version-16-hotfix` (15 role and receipt type scenarios): 4 changed, all intended (Stock Manager with a Purchase Invoice: Get Items with and without a User Permission for its own company, and the receipt details). Every refusal (other company, Stock User, Website Manager) is the same on both sides.

### How to test

1. Create a user with only the roles **Stock Manager** and **Stock User**.
2. As Administrator, submit a Purchase Invoice with **Update Stock** checked, for a stock item.
3. As the user, create a Landed Cost Voucher. In **Vouchers**, set **Receipt Document Type** to `Purchase Invoice` and **Receipt Document** to that invoice.
4. Click **Get Items**. **Receipt Items** is filled from the invoice. Add a **Landed Cost** row and save; the voucher saves.
5. Add a User Permission for the user on another **Company**, and repeat step 4. The user is refused.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `542d37769711`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.