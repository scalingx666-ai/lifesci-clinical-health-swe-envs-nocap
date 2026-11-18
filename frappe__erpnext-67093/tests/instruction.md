# Issue

**Title:** fix(stock): check warehouse access in auto_fetch_serial_number (backport #66002)

## Description

Backport of #66002 to `version-16-hotfix`.

`auto_fetch_serial_number` picks serial numbers for the Point of Sale item details. Any desk user could list the serial numbers in any warehouse. It now checks that the user can access the warehouse.

**Fix:** `auto_fetch_serial_number` checks select permission on the warehouse with `erpnext.require_permission`. ()

**Changes compared with develop:** The code change applies to the same place. On develop the function also checks Item select permission from an earlier develop change that is not on this branch; this PR does not add it. The develop test is in `erpnext/stock/tests/test_serial_batch_identity.py`, which does not exist on this branch. The test is ported to `test_serial_no.py`: it makes its own serial item and serial numbers and uses `create_user` and `add_user_permission` instead of the develop helpers, with the same assertions. Other PRs to `version-16-hotfix` that change `serial_no.py` and `test_serial_no.py`: #67095. Both PRs add the same `from erpnext import require_permission` import; the other changes are on different lines, and each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_serial_auto_fetch_checks_warehouse_permission`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_serial_no.py` (complete file): 11 tests, 8 errors with `NamingSeries.get_current_value() takes 1 positional argument but 2 were given`. The same 8 tests fail on `version-16-hotfix` without this change (local site issue).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.