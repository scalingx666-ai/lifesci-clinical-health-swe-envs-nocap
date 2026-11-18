# Issue

**Title:** fix(manufacturing): check that Production Plan row warehouses belong to its company (backport #65926)

## Description

Backport of #65926 to `version-16-hotfix`.

A Production Plan did not check the warehouses in its rows against its Company, and on submit it wrote its reserved quantity to the Bin of each row warehouse, even when that warehouse belongs to another company. Now every warehouse on the plan must belong to the plan's Company.

**Fix:** `validate_warehouse_belongs_to_company` runs `validate_warehouse_company` on **For Warehouse**, **Sub Assembly Warehouse**, the **Assembly Items** warehouses, the sub assembly **Target Warehouse** and the **Raw Materials** **For Warehouse** and **From Warehouse**, once per distinct warehouse. () A follow-up test commit covers **For Warehouse**, **Sub Assembly Warehouse** and the raw material **From Warehouse**. ()

**Changes compared with develop:** `validate` conflicted only in context, because this branch has no `clear_stale_schedule`. The new method is placed after `validate`. #67078 and #67083 also change `production_plan.py` and `test_production_plan.py` in other places. Each merges on its own.

 for the example and the steps to test.

### Tests

- `test_row_warehouse_of_another_company_is_rejected`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_row_warehouse_of_plan_company_reserves_bin_on_submit` (must still work): passes on this branch and on `version-16-hotfix` without the fix.
- `test_production_plan.py` (complete file): 160 pass. `test_stock_reservation_of_serial_nos_against_production_plan` fails the same way on `version-16-hotfix` without this change on the local test site (`NamingSeries.get_current_value()` TypeError).
- The follow-up commit extends `test_row_warehouse_of_another_company_is_rejected` to **For Warehouse**, **Sub Assembly Warehouse** and a **Material Transfer** raw material row with another company's **From Warehouse**. The test passes on this branch. When the check of each of these three fields is removed in turn, the test fails.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.