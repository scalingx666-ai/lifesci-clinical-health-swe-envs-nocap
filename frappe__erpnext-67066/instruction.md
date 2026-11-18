# Issue

**Title:** fix(stock): check Item Tax Template permission in get_item_tax_map (backport #65909)

## Description

Backport of #65909 to `version-15-hotfix`.

`get_item_tax_map` returned the tax accounts and rates of any Item Tax Template to any logged-in user. Now the method checks that the user can select the Item Tax Template, with User Permissions applied.

**Fix:** The whitelisted `get_item_tax_map` checks select permission on the Item Tax Template and then calls the new `_get_item_tax_map`, which has the old body. The server callers (`calculate_taxes_and_totals`, `_get_item_details`, `get_item_tax_info` and `set_child_tax_template_and_map` of the Update Items dialog) call `_get_item_tax_map`, so saving a transaction does not change. ()

**Changes compared with develop:** On version 15, `get_item_tax_map` has the signature `(company, item_tax_template, as_json=True)` and not `(*, doc, tax_template, as_json)`. The whitelisted method and the new `_get_item_tax_map` keep the version 15 signature, and the callers keep their version 15 arguments. `erpnext/accounts/services/taxes.py` does not exist on version 15: `set_child_tax_template_and_map` is in `erpnext/controllers/accounts_controller.py`, so its import and call change to `_get_item_tax_map` there. The test calls `get_item_tax_map(company=..., item_tax_template=..., as_json=False)`. #67063 (backport of #65905), #67064 (backport of #65906), #67065 (backport of #65908), #67067 (backport of #65911), #67068 (backport of #65925) also change `erpnext/stock/get_item_details.py` on this branch, in other functions or tests. #67063 (backport of #65905) also changes `test_item_tax_template.py` on this branch, in other functions or tests. Each pull request merges on its own, and they all merge together without conflicts.

 for the example and the steps to test.

### Tests

- `test_item_tax_map_needs_template_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_item_tax_template.py` (complete file): 16 tests pass.
- `test_get_item_details.py` (complete file, because `_get_item_details` and `get_item_tax_info` now call `_get_item_tax_map`): 23 of 24 tests pass. `test_get_item_detail_purchase_order` fails on this local site (`price_list_rate` is 0.0, not 100). It fails the same way on `version-15-hotfix` without the change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.