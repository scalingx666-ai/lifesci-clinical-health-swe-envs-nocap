# Issue

**Title:** fix(selling): skip selling price checks for internal transfers (backport #67459)

## Description

**Problem:** with Validate Selling Price on, `validate_selling_price` skips the valuation rate check for internal customers, but runs the last purchase rate check first for every row. An internal transfer Delivery Note moves stock at the valuation rate, so it is refused whenever that rate is below the item's Last Purchase Rate, and the user cannot raise it.

**Fix:** skip both checks for internal transfers (internal customer of the same company). Inter-company sales keep the last purchase rate check.

### Steps to reproduce
1. Selling Settings: tick Validate selling price for Item against purchase or valuation rate.
2. Item with Last Purchase Rate 120 and valuation rate 89.48 in Stores.
3. Delivery Note to an internal customer of the same company, qty 1 from Stores to Goods In Transit. Save.

Before: "Selling rate ... is lower than its last purchase rate". After: it saves at the valuation rate.
<hr>This is an automatic backport of pull request #67459 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f86f1fb9d983`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.