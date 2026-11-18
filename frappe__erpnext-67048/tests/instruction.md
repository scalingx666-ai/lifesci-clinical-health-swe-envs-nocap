# Issue

**Title:** fix(controllers): check Warehouse read permission in get_warehouse_address (backport #65941)

## Description

Backport of #65941 to `version-15-hotfix`.

`get_warehouse_address` is the search behind the **Source Warehouse Address** and **Target Warehouse Address** fields of Stock Entry. It returned the addresses linked to any warehouse name in the filters, without a permission check. Now the user must be able to read the Warehouse.

**Fix:** return no rows when `warehouse` is missing or is not a string, and check read permission on the Warehouse before the addresses are read. ()

**Changes compared with develop:** The test file conflicted only because develop has other tests next to the new test. Only the new test is added. It is placed before `test_warehouse_query`. The test uses `as_user` instead of `self.set_user` and rolls back its records at the end, because the test class of this file on version 15 is `unittest.TestCase`. This PR and the other backports to `version-15-hotfix` that change `queries.py` and `test_queries.py` (#67046, #67047, #67049) change different functions and different places in the test file. Each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_warehouse_address_query_requires_warehouse_read_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_queries.py` (complete file): all tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.