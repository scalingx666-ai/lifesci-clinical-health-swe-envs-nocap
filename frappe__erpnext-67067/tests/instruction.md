# Issue

**Title:** fix(stock): check Item Tax Template permission in get_item_tax_info (backport #65911)

## Description

Backport of #65911 to `version-15-hotfix`.

`get_item_tax_info` returned the Item Tax Template and the tax accounts and rates of an Item for any Company to any logged-in user. Now the method checks that the user can select each Item Tax Template it returns, with User Permissions applied.

**Fix:** `get_item_tax_info` checks select permission once for each distinct Item Tax Template in its result. ()

**Changes compared with develop:** On version 15, each result row of `get_item_tax_info` is a plain dict, so the check reads `row.get("item_tax_template")`. The test passes `company="_Test Company"` in place of `doc={"company": "_Test Company"}`, and it is added at the end of the class. #67063 (backport of #65905), #67064 (backport of #65906), #67065 (backport of #65908), #67066 (backport of #65909), #67068 (backport of #65925) also change `erpnext/stock/get_item_details.py` on this branch, in other functions or tests. #67064 (backport of #65906), #67065 (backport of #65908) also change `erpnext/stock/tests/test_get_item_details.py` on this branch, in other functions or tests. Each pull request merges on its own, and they all merge together without conflicts.

 for the example and the steps to test.

### Tests

- `test_item_tax_info_needs_template_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_get_item_details.py` (complete file): 24 of 25 tests pass. `test_get_item_detail_purchase_order` fails on this local site (`price_list_rate` is 0.0, not 100). It fails the same way on `version-15-hotfix` without the change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.