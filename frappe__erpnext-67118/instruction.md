# Issue

**Title:** fix(stock): read the Stock Entry purpose with permissions in Quality Inspection item_query (backport #65947)

## Description

Backport of #65947 to `version-16-hotfix`.

`item_query` (the search behind **Item Code** on a Quality Inspection) read the purpose of the Stock Entry in **Reference Name** without a permission check, and accepted a reference name that was not a plain name. It now reads the purpose through `frappe.get_list`, so the user's permissions apply, and it returns nothing when the reference name is empty or not a string.

**Fix:** `item_query` reads the Stock Entry purpose with `frappe.get_list` instead of `frappe.get_cached_value`, and returns an empty list when **Reference Name** is empty or not a string. ()

**Changes compared with develop:** None. The commit applies without changes.

 for the example and the steps to test.

### Tests

- `test_item_query_for_stock_entry_respects_permissions`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_quality_inspection.py` (complete file): 33 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.