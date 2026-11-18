# Issue

**Title:** fix(stock): check Company and Stock Reconciliation access in get_difference_account (backport #65930)

## Description

Backport of #65930 to `version-15-hotfix`. The version-16 backport is #67120.

`get_difference_account` fills the **Difference Account** of a Stock Reconciliation when the **Purpose** or **Company** changes. It returned the Stock Adjustment or Temporary account of any company to any logged-in user. Now it checks that the user has access to Stock Reconciliation and can select the Company (with user permissions, also when they apply only to Stock Reconciliation).

**Fix:** At the start of `get_difference_account`, check read permission on Stock Reconciliation, select permission on the Company document, and Company user permissions with **Applicable For** `Stock Reconciliation`. ()

**Changes compared with develop:** The develop fix uses `_require_reconciliation_permission`, which an earlier develop change added for `get_items` and `get_stock_balance_for`. That change is not on this branch, so this PR adds the two small helpers `_reconciliation_allowed_docs` and `_require_reconciliation_permission` (the same code as develop) above `get_difference_account`, with their imports. The function signature on this branch has no type annotations, and it is kept. `get_items` and `get_stock_balance_for` are not changed. The two develop commits are one commit here.

 for the example and the steps to test.

### Tests

- `test_difference_account_needs_company_and_reconciliation_access`, `test_difference_account_applies_company_permission_for_stock_reconciliation`: pass on this branch, fail on `version-15-hotfix` without the fix.
- `test_stock_reconciliation.py` (complete file): 68 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1ad8592b41f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.