# Issue

**Title:** fix(stock): apply user permissions in the Serial and Batch Summary serial and batch filters (backport #66005)

## Description

Backport of #66005 to `version-15-hotfix`. The version-16 backport is #67107.

The **Serial No** and **Batch No** filters of the Serial and Batch Summary report listed every serial number or batch of the item, without the user's permissions. A user limited to one company by a User Permission could see the serial numbers of another company. The filter queries now apply the user's permissions.

**Fix:** `get_serial_nos` and `get_batch_nos` use `frappe.get_list` instead of `frappe.get_all` when they list the serial numbers or batches of an item. ()

**Changes compared with develop:** On develop both filters share `get_serial_batch_options`, which builds one `frappe.qb.get_query`, and the fix passes `ignore_permissions=False` to it. On this branch the two filters have their own `frappe.get_all` calls, so both calls are changed to `frappe.get_list`. The filters by voucher are not changed (as on develop, they already check read permission on the voucher). In the new test, the rows of this branch hold only the name (the serial number), so the test reads `row[0]` instead of `row[1]`.

 for the example and the steps to test.

### Tests

- `test_serial_filter_lists_serial_nos_of_permitted_company`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_batch_filter_lists_nothing_without_access_to_batches` (Sales User with only select permission on Batch): passes.
- `test_serial_and_batch_summary.py` (complete file): 7 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.