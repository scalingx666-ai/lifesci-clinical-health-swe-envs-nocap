# Issue

**Title:** fix(manufacturing): escape the item image in the BOM tree preview (backport #65959)

## Description

Backport of #65959 to `version-15-hotfix`. The version-16 backport is #67084.

The BOM tree view showed the item image with an unquoted `src` attribute, and the server sent the image path wrapped in SQL quotes (`frappe.db.escape`). An image path with a quote in it could change the `img` tag. Now the server sends the image path as stored, and the template quotes and escapes it.

**Fix:** Remove the `frappe.db.escape` call on the image in the BOM `get_children`, render the image in `bom_item_preview.html` as a quoted and escaped `src`, and escape the BOM and Item names in the "Open BOM" and "Open Item" buttons. ()

**Changes compared with develop:** This branch has no `bom/mapper.py`. The `frappe.db.escape` line is removed from `get_children` in `bom.py`, and the test imports `get_children` from `bom.py`. Version 15 Frappe has no `frappe.utils.bold` in JavaScript, so the BOM and Item names in the buttons use `frappe.utils.escape_html(...).bold()`. The template on this branch already used `{% if data.image %}`. The test is added at the end of `TestBOM`. #67105 also changes `bom.py` and `test_bom.py` in other places. Each merges on its own.

 for the example and the steps to test.

### Tests

- `test_bom_tree_returns_item_image_as_stored`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_bom.py` (complete file): 47 pass. `test_bom_cost_multi_uom_based_on_valuation_rate` fails the same way on `version-15-hotfix` without this change on the local test site ("_Test Disabled Warehouse - _TC" is disabled).
- Template check in node (version 15 has no JavaScript test runner, so no test file is committed): `bom_item_preview.html` is compiled with the `microtemplate.js` of Frappe version 15 and rendered with an image path that contains a double quote and with markup in the BOM and Item names. On this branch the `img` tag keeps only `class`, `style` and `src`, and the names show as text. With the template of `version-15-hotfix`, the text after the quote becomes an extra attribute of the `img` tag, and the names are rendered as markup. The version-16 backport #67084 adds this check as a test that runs with `yarn test:js`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.