# Issue

**Title:** fix(stock): accept only a text Item Code in get_item_tax_info (backport #65908)

## Description

Backport of #65908 to `version-15-hotfix`.

`get_item_tax_info` loaded each Item with whatever value it got as the Item Code of a row. When that value was not text, the method still found an Item and returned its Item Tax Template and tax rates. Now the method accepts only a text Item Code.

**Fix:** `get_item_tax_info` throws when the Item Code of a row is not text. ()

**Changes compared with develop:** On version 15, `get_item_tax_info` takes `company` and not `doc`, and each result row is a plain dict. The same check is added before the row is made. The test passes `company="_Test Company"` in place of `doc={"company": "_Test Company"}`. #67063 (backport of #65905), #67064 (backport of #65906), #67066 (backport of #65909), #67067 (backport of #65911), #67068 (backport of #65925) also change `erpnext/stock/get_item_details.py` on this branch, in other functions or tests. #67064 (backport of #65906), #67067 (backport of #65911) also change `erpnext/stock/tests/test_get_item_details.py` on this branch, in other functions or tests. Each pull request merges on its own, and they all merge together without conflicts.

 for the example and the steps to test.

### Tests

- `test_item_tax_info_needs_item_code_as_text`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_get_item_details.py` (complete file): 24 of 25 tests pass. `test_get_item_detail_purchase_order` fails on this local site (`price_list_rate` is 0.0, not 100). It fails the same way on `version-15-hotfix` without the change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.