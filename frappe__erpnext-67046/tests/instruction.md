# Issue

**Title:** fix(controllers): check Batch permission in get_batch_no (backport #65937)

## Description

Backport of #65937 to `version-15-hotfix`.

`get_batch_no` is the search behind the **Batch No** field in stock transactions. It returned batch names, quantity in stock per warehouse and manufacturing and expiry dates for any item, without a permission check. Now the user must have select permission on Batch, and the batches are read again with `frappe.get_list`, so the user's permissions on Batch apply.

**Fix:** check select permission on Batch at the start of `get_batch_no`, and keep only the batches that `frappe.get_list("Batch")` returns for the user. ()

**Changes compared with develop:**
- On develop, `get_batch_no` already reads the batch rows with `frappe.get_all("Batch")` to add the batch ID, and the fix changed that call to `frappe.get_list`. Version 15 does not have that call. The fix adds one `frappe.get_list("Batch", filters={"name": ("in", ...), "item": ...}, pluck="name")` call and drops the rows that are not in the result. The row format of version 15 does not change.
- `erpnext/stock/tests/test_serial_batch_link_queries.py` does not exist on version 15. The two develop tests are in `erpnext/controllers/tests/test_queries.py`, with the same names. They make the batches with a Stock Entry instead of the develop helpers, use `as_user` and `make_fenced_user` like the other tests of the file, and roll back their records at the end, because the test class of this file is `unittest.TestCase`. The quantity assertion uses the version 15 row format (`(batch, quantity)`).
- Other PRs to `version-15-hotfix` that change `queries.py` and `test_queries.py`: #67047, #67048, #67049. They change different functions and different places in the test file. Each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_batch_link_search_requires_batch_permission`, `test_batch_link_search_applies_batch_user_permissions`: pass on this branch, fail on `version-15-hotfix` without the fix.
- Must still work (checked with a script on this branch): users with only Sales User, Stock User, Item Manager, Accounts User or Manufacturing User still get the batch and its quantity. A user with only Purchase User gets a permission error, as on develop, because Purchase User has no permission on Batch.
- `test_queries.py` (complete file): all tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.