# Issue

**Title:** fix(stock): check receipt document access when Landed Cost Voucher gets items (backport #65857)

## Description

Backport of #65857 to `version-15-hotfix`. The version-16 backport is #67034.

The **Get Items** button of Landed Cost Voucher reads the item rows of each document in the **Vouchers** table. It used the **Receipt Document Type** and **Receipt Document** as sent by the form, without a check of the type or of read permission on the document. Now the type must be one of the supported receipt types, and the user must have read permission on the document.

**Fix:** `get_items_from_purchase_receipts` calls the new `check_receipt_document_access` for each row before it reads the items. ()

**Changes compared with develop:** `get_receipt_document_details` and `RECEIPT_DOCUMENT_TYPES` do not exist on `version-15-hotfix`. This PR adds `RECEIPT_DOCUMENT_TYPES` with the two receipt types that version 15 supports (Purchase Invoice and Purchase Receipt, the options of **Receipt Document Type**), and `check_receipt_document_access`, which `get_items_from_purchase_receipts` calls for each row. The develop conflict with `get_receipt_document_details`, and the test `test_receipt_reads_need_document_access` of another change, are left out. The Landed Cost Voucher vendor invoice search change of #65799 is not backported to version 15, because the vendor invoice search does not exist there, so this PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_get_items_needs_receipt_access`: passes on this branch, fails on `version-15-hotfix` without the fix (no error for the `Sales Invoice` type).
- `test_landed_cost_voucher.py` (complete file): 28 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.