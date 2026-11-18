# Issue

**Title:** fix(stock): accept only a text Item Code in get_item_tax_template (backport #65905)

## Description

Backport of #65905 to `version-15-hotfix`.

`get_item_tax_template` loaded the Item with whatever value it got as the Item Code. When that value was not text, the method still found an Item and returned its Item Tax Template. Now the method accepts only a text Item Code.

**Fix:** `get_item_tax_template` throws when the Item Code is not text. ()

**Changes compared with develop:** On version 15, `get_item_tax_template` takes `args` (a dict) and not `ctx`, so the check is `isinstance(args.get("item_code"), str)`. The version 15 test file has a second test class after `TestItemTaxTemplate`, so the new test is added at the end of `TestItemTaxTemplate`. #67064 (backport of #65906), #67065 (backport of #65908), #67066 (backport of #65909), #67067 (backport of #65911), #67068 (backport of #65925) also change `erpnext/stock/get_item_details.py` on this branch, in other functions or tests. #67066 (backport of #65909) also changes `test_item_tax_template.py` on this branch, in other functions or tests. Each pull request merges on its own, and they all merge together without conflicts.

 for the example and the steps to test.

### Tests

- `test_item_code_must_be_a_string_to_get_template`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_item_tax_template.py` (complete file): 16 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.