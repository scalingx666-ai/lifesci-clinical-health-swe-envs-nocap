# Issue

**Title:** fix(stock): evaluate Inventory Dimension conditions on field values instead of documents (backport #65949)

## Description

Backport of #65949 to `version-16-hotfix`.

The **Conditional Rule** of an Inventory Dimension was evaluated with the live item row and parent documents as `doc` and `parent`, so a rule could call document methods while a stock transaction was submitted. Now the rule gets plain copies of the field values of the row and of the parent. Rules that compare field values, as the **Conditional Rule Examples** describe, work as before.

**Fix:** In `get_evaluated_inventory_dimension`, give `frappe.safe_eval` a `frappe._dict` of the field values of the row and the parent (from `get_valid_dict`, plus `doctype`) instead of the documents. ()

**Changes compared with develop:** The code change applies without changes. The test conflicts only on the name of the next test method (`test_check_mandatory_depends_on_backend` on this branch), and the new test is added before it. Other PRs to `version-16-hotfix` that change `inventory_dimension.py` and `test_inventory_dimension.py`: #67114. It touches different lines, and each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_dimension_condition_reads_field_values_only`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_dimension_condition_limits_rows` and `test_inventory_dimension` (rules that compare field values): pass with and without the fix.
- `test_inventory_dimension.py` (complete file): 25 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.