# Issue

**Title:** fix(controllers): show Bin quantities in warehouse_query only to users who can read Bin (backport #65942)

## Description

Backport of #65942 to `version-15-hotfix`.

`warehouse_query` is the warehouse search in stock and sales forms. It shows the quantity in stock next to each warehouse and sorts by it. The quantity comes from Bin, but Bin permission was not checked, so users with no access to Bin (for example Website Manager) saw the quantities. Now the Bin quantity is added only for users who can read Bin.

**Fix:** join Bin, add the `Actual Qty` column and sort by quantity only when the user has read permission on Bin. Other users get the warehouse names only, sorted by name. ()

**Changes compared with develop:** On develop, `warehouse_query` is built with `frappe.qb`. On `version-15-hotfix` it is still one SQL string, and that change is not part of this backport. The same rule is ported to the SQL string: the Bin column, the Bin join with its filters and the sort by quantity are added to the string only when `frappe.has_permission("Bin", "read")` is true. The test uses `as_user` instead of `self.set_user`, because the test class of this file on version 15 is `unittest.TestCase`. This PR and the other backports to `version-15-hotfix` that change `queries.py` and `test_queries.py` (#67046, #67047, #67048) change different functions and different places in the test file. Each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_warehouse_query_shows_stock_only_with_bin_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_warehouse_query` (Bin filter): still passes.
- `test_queries.py` (complete file): all tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.