# Issue

**Title:** fix(subcontracting): link a return's secondary rows to receipt rows made before v16 (backport #66552)

## Description

Depends-On: #66400

**Problem:** With #66400, a Subcontract Return links its rebuilt secondary (scrap) rows to the receipt's rows by `bom_secondary_item`. Scrap rows received before v16 do not have `bom_secondary_item` (`co_by_product_patch` only sets `valuation_type`), so they never match. A full return then leaves the receipt at 66.67% and "Completed".

**Fix:** Keep matching by `bom_secondary_item` where the receipt row has one. Pair rows received before v16 with the BOM rows of their item by qty, per finished good row, since the migration does not keep the BOM's row order (#66663). Built on #66400; until that merges, this diff also shows its commits.

**Steps to reproduce:**
1. On v15, make a BOM for a subcontracted finished good with a scrap item, a Subcontracting Order, transfer the raw materials and submit a Subcontracting Receipt with its scrap row.
2. Upgrade to v16 / develop and migrate. (On a fresh site: clear `bom_secondary_item` on the receipt's scrap row instead.)
3. Create > Subcontract Return on that receipt, keep all qty, save and submit.

Before: the receipt stays at 66.67% and "Completed", and its scrap row keeps Returned Qty 0. After: 100% and "Return Issued".

<hr>This is an automatic backport of pull request #66552 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8ed342331912`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.