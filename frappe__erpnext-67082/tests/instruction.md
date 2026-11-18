# Issue

**Title:** fix(subcontracting): check that subcontracting warehouses belong to the document company (backport #65933)

## Description

Backport of #65933 to `version-16-hotfix`.

Subcontracting documents did not check that their warehouses belong to the document's company, because their `validate` branch in `SubcontractingController` skips the warehouse check that Purchase Order and Purchase Receipt run. Each warehouse on these documents must now belong to the document's company.

**Fix:** The subcontracting branch of `SubcontractingController.validate` checks every Warehouse link on the document and its rows against the company, after the raw material rows are filled. The raw material reset and `get_current_stock` also check the **Supplier Warehouse** before they read rates or stock from it. ()

**Changes compared with develop:** The imports of `subcontracting_controller.py` conflicted (this branch does not import `get_valuation_method` or `SerialBatchIdentity`), so only `validate_warehouse_company` is added. The test file conflicted on tests that are different on this branch; the three new tests are added after `test_draft_bom_is_refused`. The two develop commits are one commit here.

 for the example and the steps to test.

### Tests

- `test_warehouses_must_belong_to_the_order_company`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_reserve_warehouse_from_job_card_must_belong_to_the_order_company`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_receipt_supplier_warehouse_must_belong_to_the_receipt_company`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_subcontracting_order.py` (complete file): 47 pass. 7 serial and batch tests (`test_make_rm_stock_entry_for_batch_items`, `test_make_rm_stock_entry_for_batch_items_with_less_transfer`, `test_make_rm_stock_entry_for_serial_items`, `test_reservation_counts_supplied_qty`, `test_stock_reservation`, `test_alternative_item_transfer_counts_against_its_original_requirement`, `test_closing_releases_unused_batches_of_partly_transferred_reservation`) fail the same way on `version-16-hotfix` without this change on the local test site (`NamingSeries.get_current_value()` TypeError).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.