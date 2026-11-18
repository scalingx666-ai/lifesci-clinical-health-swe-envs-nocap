# Issue

**Title:** fix(manufacturing): cost a BOM row at the last valuation rate when its source warehouse has no stock

## Description

With Rate of Materials based on Valuation Rate, a BOM row whose Source Warehouse has never held the item gets the Item master valuation rate (often 0). The Bin query returns None for that warehouse, and the fallback to the last stock ledger valuation rate ran only for 0 or less, not for None.

Fix: use the last valuation rate when the warehouse average is None too.

Steps to reproduce:
1. Create a stock item RM with Valuation Rate 0. Make a Material Receipt of 10 RM at 50 into Stores.
2. Create a BOM with Rate of Materials based on Valuation Rate and one row: RM, qty 1, Source Warehouse "Work In Progress" (RM was never there). Save.
3. The row rate is 0. It should be 50, the same as with no Source Warehouse.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b196c7d39c33`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.