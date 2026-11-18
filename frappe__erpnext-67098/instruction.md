# Issue

**Title:** fix(manufacturing): apply Company user permissions in Work Order Consumed Materials report (backport #65796)

## Description

Backport of #65796 to `version-15-hotfix`. The version-16 backport is #67077.

The Work Order Consumed Materials report read Work Orders without the user's Company user permissions, so a user restricted to one company could see the Work Orders and raw material quantities of another company. The report now lists only Work Orders of the companies the user is permitted to see.

**Fix:** The Work Order query adds a condition for the companies that the user's Company user permissions allow. ()

**Changes compared with develop:** This branch has no `company_restriction.py` (`get_allowed_companies_condition`), and `frappe.get_all` on version 15 does not take query builder conditions in its filters. The report gets the allowed companies from the user's Company user permissions with `get_allowed_docs_for_doctype` (new `get_allowed_companies` in the report file), turns the filters into a filter list with `make_filter_tuple`, and adds a `company in (...)` filter. The test makes its Work Order in the test, because this branch does not have the `make_manufactured_work_order` helper.

 for the example and the steps to test.

### Tests

- `test_company_user_permission_limits_work_orders`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_work_order_consumed_materials.py` (complete file): 4 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.