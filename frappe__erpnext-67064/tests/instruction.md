# Issue

**Title:** fix(stock): accept only a text Item Code in calculate_service_end_date (backport #65906)

## Description

Backport of #65906 to `version-15-hotfix`.

`calculate_service_end_date` loaded the Item with whatever value it got as the Item Code. When that value was not text, the method still found an Item and returned its deferred revenue details. Now the method accepts only a text Item Code.

**Fix:** `calculate_service_end_date` throws when the Item Code is not text. ()
- Follow-up: The check also runs when the caller passes an `item`, because `get_default_deferred_account` reads the Item defaults with the same Item Code. ()

**Changes compared with develop:** On version 15, `calculate_service_end_date` takes `args` and calls `process_args`, so the same check is on `args.item_code`. The follow-up commit is not on develop: there, the `item: Document | None` type annotation of `calculate_service_end_date` already refuses a dict `item` from a request. #67063 (backport of #65905), #67065 (backport of #65908), #67066 (backport of #65909), #67067 (backport of #65911), #67068 (backport of #65925) also change `erpnext/stock/get_item_details.py` on this branch, in other functions or tests. #67065 (backport of #65908), #67067 (backport of #65911) also change `erpnext/stock/tests/test_get_item_details.py` on this branch, in other functions or tests. Each pull request merges on its own, and they all merge together without conflicts.

 for the example and the steps to test.

### Tests

- `test_service_end_date_needs_item_code_as_text`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_service_end_date_needs_item_code_as_text_when_item_is_given`: passes on this branch, fails without the follow-up commit.
- `test_get_item_details.py` (complete file): 25 of 26 tests pass. `test_get_item_detail_purchase_order` fails on this local site (`price_list_rate` is 0.0, not 100). It fails the same way on `version-15-hotfix` without the change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.