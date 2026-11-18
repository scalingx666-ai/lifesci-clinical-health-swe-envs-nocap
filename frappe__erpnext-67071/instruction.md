# Issue

**Title:** fix(controllers): check Item and Item Tax Template permissions in get_tax_template (backport #65935)

## Description

Backport of #65935 to `version-15-hotfix`.

`get_tax_template` is the search behind the **Item Tax Template** field in the items table of sales and purchase transactions. It loaded the Item from the value of `item_code` in the filters without a permission check, and it returned the templates of that Item for any company given in the filters. Now the item code must be a single name, the user must be able to read the Item, and the result contains only the Item Tax Templates that the user can see.

**Fix:** Accept only a plain name in `item_code` and `item_group`, check read permission on the Item, and pass the templates found on the Item and its Item Groups through `frappe.get_list`, so the user's permissions on Item Tax Template apply. The two develop commits are one commit here. ()

**Changes compared with develop:** The two develop commits are one commit here. Version 15 has `get_tax_template(doctype, txt, searchfield, start, page_len, filters)` without type annotations, and the signature stays as it is. Version 15 builds the context as a plain `args` dict; only the `item_code` value changes there. On version 15, `TestQueries` is a `unittest.TestCase` without `set_user` and without a rollback, so the tests use `as_user`, and the user with the Company User Permission is made with `make_fenced_user`, which replaces its User Permissions on each run. #67070 (backport of #65934) also changes `erpnext/controllers/queries.py` and `erpnext/controllers/tests/test_queries.py` on this branch, in other functions or tests. Each pull request merges on its own, and they all merge together without conflicts.

 for the example and the steps to test.

### Tests

- `test_tax_template_query_requires_item_read_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_tax_template_query_applies_company_user_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_queries.py` (complete file): 15 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.