# Issue

**Title:** fix(stock): refuse Stock Entry references to documents of another company (backport #65952)

## Description

Backport of #65952 to `version-16-hotfix`.

A Stock Entry did not check that the Work Order, Job Card, Pick List, Purchase Order, Subcontracting Order, Subcontracting Inward Order, outgoing or source Stock Entry and row Material Requests it names belong to its own company, and that a row's Pick List Item or Job Card Item is a row of its own **Pick List** or **Job Card**. On submit it updates those documents. The Stock Entry now refuses such references when it is saved.

**Fix:** new `validate_reference_companies` and `validate_row_reference_parents` in `StockEntry.validate` read the company of each referenced document (one query for each doctype) and the parent of each Pick List Item and Job Card Item row (one query for each child doctype), and throw when they do not match. ()

**Changes compared with develop:** The cherry-pick conflicts because `stock_entry.py` on develop has a different structure. The change is ported by hand: the two checks run at the start of `StockEntry.validate`, before the Work Order is loaded (on develop they run before the purpose class validation, at the same step). The two develop commits are one commit here. The Stock Entry tests are in `TestStockEntry` (this branch has no `TestStockEntryCoverage` class), and import `make_stock_entry` from `work_order.work_order` and `create_stock_entry` from `pick_list.pick_list` instead of the develop-only `mapper` modules. Other PRs to `version-16-hotfix` that change `stock_entry.py` and `test_stock_entry.py`: #67013, #67017, #67018. They touch different lines, and each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_stock_entry_refuses_work_order_of_other_company`, `test_stock_entry_refuses_pick_list_row_of_other_pick_list` and `test_transfer_refuses_job_card_item_of_other_job_card`: pass on this branch, fail on `version-16-hotfix` without the fix.
- `test_stock_entry.py` (complete file): 150 tests, 10 errors with `NamingSeries.get_current_value() takes 1 positional argument but 2 were given`. The same 10 tests fail on `version-16-hotfix` without this change (local site issue).
- `test_job_card.py` (complete file): 113 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.