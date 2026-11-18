# Issue

**Title:** fix(selling): compare the pending stock qty in the item indicator

## Description

**Problem:** the item indicator on a Sales Order compares `stock_qty - delivered_qty` with the stock on hand. `stock_qty` and `actual_qty` are in the stock UOM, `delivered_qty` is in the row's UOM, so a row of 2 Box (24 Nos) with 1 Box delivered compares 23 with the 15 Nos on hand and shows orange.

**Fix:** convert the delivered qty with the row's conversion factor.

### Steps to reproduce
1. Item with stock UOM Nos and UOM Box = 12; 15 Nos in Stores.
2. Submit a Sales Order for 2 Box. Deliver 1 Box, then receive 12 more Nos (15 in stock).
3. Open the Sales Order.

Before: the indicator is orange. After: green (12 Nos pending, 15 on hand).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c8576d9754e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.