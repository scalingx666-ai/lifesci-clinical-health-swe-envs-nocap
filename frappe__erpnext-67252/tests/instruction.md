# Issue

**Title:** fix(stock): add up a Material Request's received qty from qty × conversion factor whatever the setting (backport #66665)

## Description

Depends-On: #66281

Replaces #66581. Stacked on #66281: the diff shows its commits until it merges.

### Problem
With "Allow to Edit Stock UOM Qty for Purchase" off, a Purchase Receipt or stock Purchase Invoice still rounds the stock qty of each row, but the Material Request keeps its own stock qty unrounded. When you receive it in parts, the rounded rows are added up, so the received qty ends above or below the stock qty of the Material Request.

### Fix
The received qty of the Material Request now adds up qty × conversion factor of the receipt rows whatever the setting. #66281 already does this with the setting on. The total is rounded once to the field precision where the Material Request rounds its stock qty: with the setting on, or for a whole number stock UOM. The receipt rows keep their stock qty as before. A patch recalculates the received qty of Material Requests left partly received by the old sum.

### Steps to reproduce
1. Set float precision to 2. Keep "Allow to Edit Stock UOM Qty for Purchase" off.
2. Create a stock item with stock UOM Kg and UOM Box at conversion factor 0.335.
3. Submit a Material Request for 2 Box (stock qty 0.67).
4. Make two Purchase Orders from it for 1 Box each, and a Purchase Receipt from each. Submit all.

Expected: the received qty of the Material Request row is 0.67. Actual: 0.68.

<hr>This is an automatic backport of pull request #66665 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e44629d68e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.