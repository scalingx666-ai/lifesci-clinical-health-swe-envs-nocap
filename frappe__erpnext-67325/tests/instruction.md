# Issue

**Title:** test(gross profit): give copied invoice rows their own idx (backport #66907)

## Description

**Problem:** Gross Profit tests copy an invoice row with `frappe.copy_doc`, which keeps `idx`. Both rows are saved with `idx = 1`, so `make_sales_return` loads them in no fixed order. `test_return_keeps_buying_amount_of_unreturned_row` then sometimes returns the wrong row (`29999.0 != 30000`). `test_legacy_return_prefers_item_without_linked_return` has the same issue.

**Fix:** Add a test helper that clears `idx` on the copied row before `append`, so it gets `idx = 2`.

**Steps to reproduce:**
1. Run `test_return_keeps_buying_amount_of_unreturned_row` a few times.
2. Check the `idx` of the two `Sales Invoice Item` rows of its invoice: both are 1, and the test fails when the return maps the 30000 qty row first.
<hr>This is an automatic backport of pull request #66907 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8ed342331912`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.