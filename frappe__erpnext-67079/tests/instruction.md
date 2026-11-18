# Issue

**Title:** fix(portal): do not give customer portal users drop-ship Purchase Orders (backport #65922)

## Description

Backport of #65922 to `version-16-hotfix`.

A drop-ship Purchase Order stores the end customer in its **Customer** field. The portal treated that field as the party of the Purchase Order, so a customer portal user could open, print and list that Purchase Order. For documents that have a **Supplier**, the portal now uses only the supplier as the party.

**Fix:** `get_customers_suppliers` no longer returns customers for a document type that has a **Supplier** field. Both the portal page check (`has_website_permission`) and the portal list (`get_transaction_list`) read the parties from it. ()

**Changes compared with develop:** None. The commit applies without changes.

 for the example and the steps to test.

### Tests

- `test_customer_portal_user_cannot_open_drop_ship_purchase_order`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_customer_portal_list_leaves_out_drop_ship_purchase_order`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_supplier_portal_user_still_sees_drop_ship_purchase_order` (must still work): passes on this branch and on `version-16-hotfix` without the fix.
- `test_website_list_for_contact.py` (complete file): 8 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.