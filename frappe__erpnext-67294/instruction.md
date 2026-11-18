# Issue

**Title:** fix(stock): let a Stock Manager get Landed Cost Voucher items from a Purchase Invoice (backport #67292)

## Description

Issue: #67246. Backport of #67292 to `version-15-hotfix`.

#67060 made **Get Items** on a Landed Cost Voucher check **read** permission on each receipt document. The Stock Manager role, the only standard role that can create a Landed Cost Voucher, has only **Select** permission on Purchase Invoice. So a Stock Manager could pick a Purchase Invoice in **Vouchers**, but could not get its items or save the voucher.

**Example:**
- **Setup:** a user with only the roles **Stock Manager** and **Stock User**. A submitted Purchase Invoice for `_Test Company` with **Update Stock** checked, 2 of a stock item at 100.
- **Steps:**
   1. As that user, create a Landed Cost Voucher for `_Test Company`.
   2. In **Vouchers**, set **Receipt Document Type** to `Purchase Invoice` and **Receipt Document** to the invoice.
   3. Click **Get Items**.
- **Before the fix:** "No permission for Purchase Invoice". Saving the voucher fails with the same message.
- **After the fix:** **Receipt Items** has the invoice row (2 of the item), as before #67060.

**Fix:** `check_receipt_document_access` now checks **select** permission instead of **read**. In Frappe, select permission on a document is also given by read permission, and it still applies User Permissions. A user restricted to another company, or a user with no permission on Purchase Invoice, is still refused. ()

**Test order fix:** this PR adds one test, so the parallel test runner splits the test files at a different place. `test_bom_variance_report.py` then runs first in its group, before any test makes the BOM test records, and fails with "Value missing for Work Order: BOM No". In the same group, `test_sales_order.py` left negative stock of `_Test Item` in `_Test Warehouse - _TC`: two of its steps commit mid-class (`make_purchase_order_for_default_supplier` and the workflow insert), so stock moved by earlier tests in the class stays. The Delivery Note, Delivery Trip, Inventory Dimension and Material Request tests later in the group then failed with "Insufficient Stock". `test_bom_variance_report.py` now declares the BOM test records it needs, and `TestSalesOrder` rolls back after each test. These are test changes only. ()

**Changes compared with develop:** this branch has no `get_receipt_document_details`, so the change to `test_receipt_reads_need_document_access` in #67292 does not apply here.

### Tests

- `test_stock_manager_gets_items_from_purchase_invoice`: a Stock Manager gets the items from a Purchase Invoice. A Stock Manager restricted to `_Test Company 1` and a Stock User are still refused. Fails on `version-15-hotfix` without the fix, passes with it.
- `test_landed_cost_voucher.py` (complete file): 29 tests pass.
- Differential run on v15br4.localhost (11 role and receipt type scenarios):
  - against `version-15-hotfix`: 3 changed, all intended (Stock Manager with a Purchase Invoice). Every refusal is the same.
  - against `b456e4e1f1` (before #67060): every valid flow is the same. Only the 4 refusals that #67060 added differ (a Stock Manager restricted to another company, for a Purchase Invoice and a Purchase Receipt; a Stock User and a Website Manager for a Purchase Invoice).

### How to test

1. Create a user with only the roles **Stock Manager** and **Stock User**.
2. As Administrator, submit a Purchase Invoice with **Update Stock** checked, for a stock item.
3. As the user, create a Landed Cost Voucher. In **Vouchers**, set **Receipt Document Type** to `Purchase Invoice` and **Receipt Document** to that invoice.
4. Click **Get Items**. **Receipt Items** is filled from the invoice. Add a **Landed Cost** row and save; the voucher saves.
5. Add a User Permission for the user on another **Company**, and repeat step 4. The user is refused.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0a354fbd736`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.