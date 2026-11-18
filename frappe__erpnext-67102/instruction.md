# Issue

**Title:** fix(projects): do not let customer portal users print the Project (backport #65927)

## Description

Backport of #65927 to `version-15-hotfix`. The version-16 backport is #67081.

The Project was registered in the `has_website_permission` hook so that the `/projects` portal page could check the customer's access. Frappe's print view also accepts that hook, so a customer portal user could print the whole Project, with its costing and margin fields, which the portal page does not show. The portal page now calls the same check directly, and the Project is no longer in the hook.

**Fix:** `validate_and_get_project_user` calls `has_website_permission` from `website_list_for_contact` directly, and `Project` is removed from the `has_website_permission` hook in `hooks.py`. ()

**Changes compared with develop:** None. The commit applies without changes.

 for the example and the steps to test.

### Tests

- `test_customer_portal_user_cannot_print_own_customer_project`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_projects.py` (complete file): 8 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.