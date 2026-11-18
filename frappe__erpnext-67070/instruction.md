# Issue

**Title:** fix(controllers): check permissions on linked document filters in get_filtered_child_rows (backport #65934)

## Description

Backport of #65934 to `version-15-hotfix`.

`get_filtered_child_rows` is the search behind the item pickers in the stock reservation dialogs. It checked that the user can read the parent document, but then ran the search without permission checks, so a filter on a field of a linked document (for example the Sales Order of a Purchase Order Item row) was joined to that document without any check. Now a filter on a linked document needs read access to that document.

**Fix:** Before the query runs, the new `check_linked_filter_permissions` looks at each filter key that has a dot. The part before the dot must be a Link field of the child table, and the user must have read permission on the linked doctype. If not, the search stops with a permission error. Filters on fields of the child table work as before. ()

**Changes compared with develop:** The develop fix passes `ignore_permissions=False` and `parent_doctype` to `frappe.get_query`. The version 15 `frappe.get_query` does not have these arguments and does not check permissions on the fields in the filters, so the check is done in erpnext with the small helper above. The develop query engine also checks the permission level of the linked field; this port checks read permission on the linked doctype only. The callers (the stock reservation dialogs of the Sales Order) pass only `parent`, `parenttype` and `reserve_stock`. On version 15, `TestQueries` is a `unittest.TestCase` without `set_user`, so the test uses `as_user`. Because this port is not the develop code, the test also checks that a user with the Purchase User and Sales User roles can still filter on `sales_order.grand_total` and gets the row. #67071 (backport of #65935) also changes `erpnext/controllers/queries.py` and `erpnext/controllers/tests/test_queries.py` on this branch, in other functions or tests. Each pull request merges on its own, and they all merge together without conflicts.

 for the example and the steps to test.

### Tests

- `test_get_filtered_child_rows_checks_linked_document_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_queries.py` (complete file): 14 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ccd5ab90f7dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.