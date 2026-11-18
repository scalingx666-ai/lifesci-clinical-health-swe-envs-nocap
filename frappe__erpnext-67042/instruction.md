# Issue

**Title:** fix(buying): check Supplier Group read permission in get_supplier_group_details (backport #65943)

## Description

Backport of #65943 to `version-16-hotfix`.

When a user picked a **Supplier Group** on a Supplier, `get_supplier_group_details` copied the **Accounts** and the **Default Payment Terms Template** of that Supplier Group even when the user could not read the Supplier Group. Now the method checks read permission on the Supplier Group.

**Fix:** load the Supplier Group with `check_permission="read"`. ()

**Changes compared with develop:** None. The commit applies without changes.

 for the example and the steps to test.

### Tests

- `test_supplier_group_details_need_supplier_group_read_permission`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_supplier.py` (complete file): all tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.