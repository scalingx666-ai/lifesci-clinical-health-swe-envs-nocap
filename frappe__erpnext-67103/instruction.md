# Issue

**Title:** fix(subcontracting): check that subcontracting warehouses belong to the document company (backport #65933)

## Description

Backport of #65933 to `version-15-hotfix`. The version-16 backport is #67082.

Subcontracting documents did not check that their warehouses belong to the document's company, because their `validate` branch in `SubcontractingController` skips the warehouse check that Purchase Order and Purchase Receipt run. Each warehouse on these documents must now belong to the document's company.

**Fix:** The subcontracting branch of `SubcontractingController.validate` checks every Warehouse link on the document and its rows against the company, after the raw material rows are filled. The raw material reset and `get_current_stock` also check the **Supplier Warehouse** before they read rates or stock from it. ()

**Changes compared with develop:** On this branch the method is `create_raw_materials_supplied` (develop: `create_raw_materials_supplied_or_received`), and Subcontracting Inward Order does not exist. The checks are added in the same places. The imports conflicted, so only `validate_warehouse_company` is added. On this branch the **Reserve Warehouse** is not filled from a Job Card, so `test_reserve_warehouse_from_job_card_must_belong_to_the_order_company` of the follow-up commit is left out. The code change of that commit (the check runs after the raw material rows are filled) is kept. The two develop commits are one commit here.

 for the example and the steps to test.

### Tests

- `test_warehouses_must_belong_to_the_order_company`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_receipt_supplier_warehouse_must_belong_to_the_receipt_company`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_subcontracting_order.py` (complete file): 36 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.