# Issue

**Title:** fix(stock): check Item read permission in get_alternative_items (backport #65931)

## Description

Backport of #65931 to `version-15-hotfix`.

`get_alternative_items` returned the alternative items of any Item to any logged-in user. Now the method checks that the user can read the Item.

**Fix:** `get_alternative_items` checks read permission on the Item in `filters.item_code` before it searches. ()

**Changes compared with develop:** Version 15 still has the SQL version of `get_alternative_items` (develop changed it to two `frappe.get_all` calls). The same `erpnext.require_permission("Item", ...)` line is added at the top of the version 15 function. The test file on version 15 does not have the `make_item_alternative` helper, so the test adds the develop helper and imports `random_string` and `get_alternative_items`. The SQL query returns tuples, so the test compares `[list(row) for row in results]` with `[[expected]]`.

 for the example and the steps to test.

### Tests

- `test_get_alternative_items_needs_item_read_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_item_alternative.py` (complete file): 6 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.