# Issue

**Title:** fix(manufacturing): check Blanket Order read permission in apply_price_list (backport #65958)

## Description

Backport of #65958 to `version-16-hotfix`.

`apply_price_list` of Blanket Order returned Item Price rates for a Blanket Order built by the caller, with no permission check. Now the method checks read permission on the Blanket Order, with User Permissions applied, and select permission on the Customer or Supplier, as `get_item_details.apply_price_list` already does.

**Fix:** call `doc.check_permission("read")` and `validate_pricing_parties(doc)` before the price list is applied. ()

Follow-up test commit: covers the party check and User Permissions. ()

**Changes compared with develop:** The fix commit applies without changes. The follow-up test commit is not in #65958.

 for the example and the steps to test.

### Tests

- `test_applying_price_list_needs_blanket_order_read_permission`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_applying_price_list_checks_party_and_user_permissions` (follow-up commit): for a Selling and a Purchasing Blanket Order, a user who can read Blanket Order but not the Customer or Supplier, a user restricted by a Company User Permission, and a user restricted by a Customer or Supplier User Permission to another party all get a permission error. A user whose User Permission allows the party still gets the same rate. The cases for the Customer or Supplier fail when `validate_pricing_parties(doc)` is removed.
- `test_blanket_order.py` (complete file): all tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.