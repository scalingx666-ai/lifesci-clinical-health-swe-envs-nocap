# Issue

**Title:** fix(manufacturing): check Company permission in Work Order get_default_warehouse (backport #66011)

## Description

Backport of #66011 to `version-16-hotfix`.

`get_default_warehouse` in Work Order returned the default Work In Progress, Finished Goods and Scrap warehouses of any company to any logged-in user. It now checks that the user can select the Company, which also applies the user's Company User Permissions.

**Fix:** `get_default_warehouse` calls `require_permission("Company", company, "select")` before it reads the defaults. ()

**Changes compared with develop:** The imports conflicted, because `work_order.py` on this branch does not import from `erpnext`; `from erpnext import require_permission` is added. The signature `get_default_warehouse(company)` of this branch is kept.

 for the example and the steps to test.

### Tests

- `test_default_warehouse_follows_company_user_permission`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_work_order.py` (complete file): 213 pass. 11 serial number tests fail the same way on `version-16-hotfix` without this change on the local test site (`NamingSeries.get_current_value()` TypeError), and `test_job_card` fails the same way on `version-16-hotfix` without this change (Workstation Type Welding Bay has no enabled Workstation on the local test site).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e5a6f383ce3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.