# Issue

**Title:** fix(stock): check Inventory Dimension read permission in get_parent_fields (backport #65944)

## Description

Backport of #65944 to `version-16-hotfix`.

`get_parent_fields` lists the parent document fields for the **Fetch Value From** field of the Inventory Dimension form. It did not check any permission, so any desk user could call it. It now needs read permission on Inventory Dimension.

**Fix:** `get_parent_fields` checks read permission on Inventory Dimension before it reads the fields. ()

**Changes compared with develop:** The cherry-pick conflicts on the function signature, because develop has type annotations on `get_parent_fields` that this branch does not have. The signature of this branch is kept and only the permission check is added. The test import conflicts with `get_inventory_dimensions`, and both imports are kept. Other PRs to `version-16-hotfix` that change `inventory_dimension.py` and `test_inventory_dimension.py`: #67116. It touches different lines, and each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_parent_fields_need_inventory_dimension_access`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_inventory_dimension.py` (complete file): 25 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.