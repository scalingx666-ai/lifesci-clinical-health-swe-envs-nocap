# Issue

**Title:** fix(stock): check Work Order, BOM and source Stock Entry read in Stock Entry get_items (backport #65929)

## Description

Backport of #65929 to `version-15-hotfix`. The version-16 backport is #67017.

**Get Items** and **Update Rate and Availability** on a Stock Entry copy rows from the Work Order, BOM or source Stock Entry named on the form. They did not check that the user can read that document. They now check read permission on the Work Order, BOM No and Source Stock Entry (Manufacture) first.

**Fix:** `StockEntry.get_items` and `StockEntry.get_stock_and_rate` check read permission on the Work Order, BOM and Source Stock Entry before they load them. `get_stock_and_rate` also checks the BOM that it takes from the Work Order, and **Get Items** for a Disassemble checks the submitted Manufacture entries of the Work Order when **Source Stock Entry (Manufacture)** is empty. ()

**Fix (follow-up):** `get_items_for_disassembly` checks every submitted Manufacture entry of the Work Order (the earlier limit of 2 is removed), and `get_items` checks read permission on the BOM that `set_work_order_details` takes from the Work Order. ()

**Changes compared with develop:** The cherry-pick conflicts because develop moved the Disassemble code to `services/disassemble.py` and the purpose logic to purpose classes. On this branch:
- `check_source_documents_permission` is called at the start of `StockEntry.get_items` (after the Pick List return) and of `StockEntry.get_stock_and_rate`.
- The Manufacture entry check is in `StockEntry.get_items_for_disassembly`, in the same place where it looks for the Manufacture entries of the Work Order. This branch read at most 2 entries there (`limit_page_length=2`); the follow-up commit removes that limit, so every entry is checked, as on develop.
- The two develop commits are one commit here.
- Tests are in `TestStockEntry` (this branch has no `TestStockEntryCoverage` class), and import `make_stock_entry` from `work_order.work_order` instead of the develop-only `work_order.mapper`, and use `change_settings` from `frappe.tests.utils` instead of `ERPNextTestSuite.change_settings`.
- The follow-up commit has no develop equivalent: develop checks every Manufacture entry already, and develop `get_items` does not copy the Work Order BOM into **BOM No** (it reads the Work Order rows instead), so it does not read a BOM that was not checked.
- Other PRs to `version-15-hotfix` that change `stock_entry.py` and `test_stock_entry.py`: #67054, #67091, #67092. They touch different lines, and each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_get_items_checks_work_order_and_bom_permission`, `test_disassemble_get_items_checks_manufacture_entry_permission`, `test_get_stock_and_rate_checks_bom_of_work_order`: pass on this branch, fail on `version-15-hotfix` without the fix.
- `test_disassemble_get_items_checks_every_manufacture_entry` (three Manufacture entries, the oldest one not readable) and `test_get_items_checks_bom_of_work_order` (Manufacture with an empty **BOM No** and a Work Order whose BOM is not readable): pass on this branch, fail on this branch without the follow-up commit.
- `test_stock_entry.py` (complete file): 134 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.