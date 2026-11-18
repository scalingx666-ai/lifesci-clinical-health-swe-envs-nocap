# Issue

**Title:** fix(stock): apply user permissions in the Serial and Batch Summary serial and batch filters (backport #66005)

## Description

Backport of #66005 to `version-16-hotfix`.

The **Serial No** and **Batch No** filters of the Serial and Batch Summary report listed every serial number or batch of the item, without the user's permissions. A user limited to one company by a User Permission could see the serial numbers of another company. The filter queries now apply the user's permissions.

**Fix:** `get_serial_nos` and `get_batch_nos` use `frappe.get_list` instead of `frappe.get_all` when they list the serial numbers or batches of an item. ()

**Changes compared with develop:** On develop both filters share `get_serial_batch_options`, which builds one `frappe.qb.get_query`, and the fix passes `ignore_permissions=False` to it. On this branch the two filters have their own `frappe.get_all` calls, so both calls are changed to `frappe.get_list`. The filters by voucher are not changed (as on develop, they already check read permission on the voucher). In the new test, the rows of this branch hold only the name (the serial number), so the test reads `row[0]` instead of `row[1]`. In `make_open_pos_invoice` of the same test file, the test user is set back to Administrator after the test, because the POS tests that run before the new test left the session user as `test@example.com`.

 for the example and the steps to test.

### Tests

- `test_serial_filter_lists_serial_nos_of_permitted_company`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_batch_filter_lists_nothing_without_access_to_batches` (Sales User with only select permission on Batch): passes.
- `test_serial_and_batch_summary.py` (complete file): 8 tests, 3 errors with `NamingSeries.get_current_value() takes 1 positional argument but 2 were given`. The same 3 tests fail on `version-16-hotfix` without this change (local site issue).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.