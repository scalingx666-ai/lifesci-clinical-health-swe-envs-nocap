# Issue

**Title:** fix(stock): refresh reconciliation amounts when qty or rate is set to 0 (backport #67444)

## Description

**Problem:** `set_amount_quantity` in the Stock Reconciliation form runs only when both qty and valuation rate are non-zero, so writing stock off to 0 leaves Amount, Quantity Difference and Amount Difference at their old values until save.

**Fix:** always recompute them; the server already does the same on save.

### Steps to reproduce
1. Item with 15 @ 100 in Stores.
2. New Stock Reconciliation, add a row for the item in Stores (15 @ 100, Amount 1,500).
3. Set Quantity to 0.

Before: Amount 1,500, differences 0. After: Amount 0, Quantity Difference -15, Amount Difference -1,500.
<hr>This is an automatic backport of pull request #67444 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06107678248e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.