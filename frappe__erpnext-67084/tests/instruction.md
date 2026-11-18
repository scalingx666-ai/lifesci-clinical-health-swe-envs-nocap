# Issue

**Title:** fix(manufacturing): escape the item image in the BOM tree preview (backport #65959)

## Description

Backport of #65959 to `version-16-hotfix`.

The BOM tree view showed the item image with an unquoted `src` attribute, and the server sent the image path wrapped in SQL quotes (`frappe.db.escape`). An image path with a quote in it could change the `img` tag. Now the server sends the image path as stored, and the template quotes and escapes it.

**Fix:** Remove the `frappe.db.escape` call on the image in the BOM `get_children`, render the image in `bom_item_preview.html` as a quoted and escaped `src`, and escape the BOM and Item names in the "Open BOM" and "Open Item" buttons. () A follow-up test commit renders the template with a double quote in the image path and markup in the BOM and Item names. ()

**Changes compared with develop:** This branch has no `bom/mapper.py`. The `frappe.db.escape` line is removed from `get_children` in `bom.py`, and the test imports `get_children` from `bom.py`. The test is added at the end of `TestBOM`. #67089 also changes `bom.py` and `test_bom.py` in other places. Each merges on its own.

 for the example and the steps to test.

### Tests

- `test_bom_tree_returns_item_image_as_stored`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_bom.py` (complete file): 71 pass.
- `erpnext/tests/js/bom_item_preview.test.mjs` (new, runs with `yarn test:js`): renders `bom_item_preview.html` with an image path that contains a double quote and with markup in the BOM and Item names. It checks that the `img` tag keeps only `class`, `style` and `src`, that `src` holds the full path, and that the names show as text. 3 pass on this branch. With the template of `version-16-hotfix`, the image and the button tests fail. The same check with the `microtemplate.js` of Frappe version 16 gives the same results. `yarn test:js` (all files): 16 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.