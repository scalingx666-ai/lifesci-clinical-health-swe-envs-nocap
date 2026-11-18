# Issue

**Title:** fix(stock): check Item read permission in get_item_manufacturer_part_no (backport #65925)

## Description

Backport of #65925 to `version-15-hotfix`.

`get_item_manufacturer_part_no` returned the Manufacturer Part Number of an Item to any logged-in user. Now the method checks that the user can read the Item.

**Fix:** The whitelisted `get_item_manufacturer_part_no` checks read permission on the Item and then calls the new `_get_item_manufacturer_part_no`, which has the old body. `get_basic_details` in `get_item_details.py` calls `_get_item_manufacturer_part_no`, because `_get_item_details` already checks the Item. ()
- Follow-up: Test only: a Purchase User whose User Permission allows one other Item is refused for this Item and still gets the part number of the permitted Item. ()

**Changes compared with develop:** Version 15 has `get_item_manufacturer_part_no(item_code, manufacturer)` without type annotations. Both functions keep the version 15 signature. In `get_basic_details` the version 15 call passes `args.get("item_code")` and `args.get("manufacturer")`, and only the function name changes. #67063 (backport of #65905), #67064 (backport of #65906), #67065 (backport of #65908), #67066 (backport of #65909), #67067 (backport of #65911) also change `erpnext/stock/get_item_details.py` on this branch, in other functions or tests. Each pull request merges on its own, and they all merge together without conflicts.

 for the example and the steps to test.

### Tests

- `test_part_no_needs_item_read_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_part_no_applies_item_user_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_item_manufacturer.py` (complete file): 8 tests pass.
- `test_get_item_details.py` (complete file, because `get_basic_details` now calls `_get_item_manufacturer_part_no`): 23 of 24 tests pass. `test_get_item_detail_purchase_order` fails on this local site (`price_list_rate` is 0.0, not 100). It fails the same way on `version-15-hotfix` without the change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.