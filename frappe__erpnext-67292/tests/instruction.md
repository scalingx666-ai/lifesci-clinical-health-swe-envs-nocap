# Issue

**Title:** fix(stock): let a Stock Manager get Landed Cost Voucher items from a Purchase Invoice

## Description

Issue: #67246 (reported on `version-15-hotfix`). The same change for `version-16-hotfix` is #67293 and for `version-15-hotfix` is #67294; each merges on its own.

#65857 made **Get Items** on a Landed Cost Voucher check **read** permission on each receipt document. The Stock Manager role, the only standard role that can create a Landed Cost Voucher, has only **Select** permission on Purchase Invoice. So a Stock Manager could pick a Purchase Invoice in **Vouchers**, but could not get its items or save the voucher. The same check, added earlier by #60207, also refused the supplier, date and total that the form fetches when a **Receipt Document** is set.

**Example:**
- **Setup:** a user with only the roles **Stock Manager** and **Stock User**. A submitted Purchase Invoice for `_Test Company` with **Update Stock** checked, 2 of a stock item at 100.
- **Steps:**
   1. As that user, create a Landed Cost Voucher for `_Test Company`.
   2. In **Vouchers**, set **Receipt Document Type** to `Purchase Invoice` and **Receipt Document** to the invoice.
   3. Click **Get Items**.
- **Before the fix:** setting **Receipt Document** shows "No permission for Purchase Invoice", and **Get Items** and saving the voucher fail with the same message.
- **After the fix:** the row shows the supplier, posting date and grand total, and **Receipt Items** has the invoice row (2 of the item).

**Fix:** `check_receipt_document_access` now checks **select** permission instead of **read**. In Frappe, select permission on a document is also given by read permission, and it still applies User Permissions. This applies to **Get Items**, to saving the voucher, and to the receipt details that the form fetches. A user restricted to another company, or a user with no permission on the receipt document type, is still refused. ()

**Note for reviewers:** `test_receipt_reads_need_document_access` (from #60207) expected a Stock Manager to be refused the details of a Purchase Invoice. It now expects a Stock User (no permission on Purchase Invoice) to be refused, and a Stock Manager to get the details. `get_vendor_invoice_amount` and the vendor invoice search keep their read check; this PR does not change them.

### Tests

- `test_stock_manager_gets_items_from_purchase_invoice`: a Stock Manager gets the items from a Purchase Invoice. A Stock Manager restricted to `_Test Company 1` and a Stock User are still refused. Fails on `develop` without the fix, passes with it.
- `test_get_items_needs_receipt_access` (from #65857): still passes.
- `test_landed_cost_voucher.py` (complete file): all pass except `test_landed_cost_voucher_for_serialized_item`, which fails on this local site with a naming series error and fails the same way on `develop`.
- Differential run on brtest3.localhost against `develop` (15 role and receipt type scenarios): 4 changed, all intended (Stock Manager with a Purchase Invoice: Get Items with and without a User Permission for its own company, and the receipt details). Every refusal (other company, Stock User, Website Manager) is the same on both sides.

### How to test

1. Create a user with only the roles **Stock Manager** and **Stock User**.
2. As Administrator, submit a Purchase Invoice with **Update Stock** checked, for a stock item.
3. As the user, create a Landed Cost Voucher. In **Vouchers**, set **Receipt Document Type** to `Purchase Invoice` and **Receipt Document** to that invoice.
4. Click **Get Items**. **Receipt Items** is filled from the invoice.
5. Add a User Permission for the user on another **Company**, and repeat step 4. The user is refused.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f52cd39ca6a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.