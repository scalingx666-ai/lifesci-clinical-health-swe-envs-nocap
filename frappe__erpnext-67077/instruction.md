# Issue

**Title:** fix(manufacturing): apply Company user permissions in Work Order Consumed Materials report (backport #65796)

## Description

Backport of #65796 to `version-16-hotfix`.

The Work Order Consumed Materials report read Work Orders without the user's Company user permissions, so a user restricted to one company could see the Work Orders and raw material quantities of another company. The report now lists only Work Orders of the companies the user is permitted to see.

**Fix:** The Work Order query adds a condition for the companies that the user's Company user permissions allow. ()

**Changes compared with develop:** `get_allowed_companies_condition` does not exist on this branch. The report uses the existing `get_allowed_companies` from `company_restriction.py` and adds `company.isin(...)` to the Work Order filters.

 for the example and the steps to test.

### Tests

- `test_company_user_permission_limits_work_orders`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_work_order_consumed_materials.py` (complete file): 4 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.