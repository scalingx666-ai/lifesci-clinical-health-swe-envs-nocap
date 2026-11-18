# Issue

**Title:** fix(manufacturing): Work Order required item rate per stock UOM (backport #67336)

## Description

For a single-level BOM, `get_bom_items_as_dict` returned the qty in stock UOM but the rate per BOM row UOM. A Work Order made from a BOM row of 1 Box (12 Nos) at 10 per Nos showed 12 Nos at 120, amount 1,440.

Fix: return the rate per stock UOM when the qty is in stock UOM. Callers that ask for the row UOM qty (Stock Entry) still get the row UOM rate.

Steps to reproduce:
1. Create item RM with stock UOM Nos and UOM Box = 12 Nos, valued at 10 per Nos.
2. Create and submit a BOM with one row: RM, qty 1, UOM Box.
3. Create a Work Order for 1 with "Use Multi-Level BOM" off. Required Items shows 12 Nos at 120, amount 1,440. It should be 10 and 120, as with "Use Multi-Level BOM" on.

<hr>This is an automatic backport of pull request #67336 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b564e4834aa1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.