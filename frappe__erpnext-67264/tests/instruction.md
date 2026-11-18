# Issue

**Title:** fix(controllers): check Account permission in get_income_account and get_expense_account (backport #65940)

## Description

Backport of #65940 to `version-16-hotfix`.

`get_income_account` and `get_expense_account` are the searches behind the **Income Account** and **Expense Account** fields (Sales Invoice, Purchase Invoice, Purchase Order, Purchase Receipt, Item, Item Group and Brand). They applied User Permissions, but did not check that the user has a role with access to Account. Now both use `frappe.qb.get_query` with `ignore_permissions=False`, like `tax_account_query` in the same file.

**Fix:** build the `get_income_account` and `get_expense_account` queries with `frappe.qb.get_query(..., ignore_permissions=False)`, which checks select permission and applies User Permissions, and remove the import of `build_qb_match_conditions`, which is no longer used. Both develop commits are in this one commit. ()

**Changes compared with develop:** The code change applies without changes. `test_queries.py` conflicted only because this branch has other tests next to the new ones; both new tests are added after the existing test of the same method, as on develop. No other open PR to `version-16-hotfix` changes `queries.py` or `test_queries.py`.

 for the example and the steps to test.

### Tests

- `test_income_account_query_requires_account_permission`, `test_expense_account_query_requires_account_permission`: pass on this branch, fail on `version-16-hotfix` without the fix.
- `test_queries.py` (complete file): all tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `851ba2edd6db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.