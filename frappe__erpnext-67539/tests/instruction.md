# Issue

**Title:** fix(stock): book rejected material that stays in transit at its stock value (backport #66966)

## Description

**Problem:** when the Rejected Warehouse of an internal Purchase Receipt is the in-transit warehouse, the row has two stock ledger entries in that warehouse (all qty out, rejected qty back in). `get_stock_value_difference` read only one of them, so the in-transit account was booked with the wrong value and sign, and the difference went to Cost of Goods Sold.

**Fix:** add up the stock value per row and warehouse. Rejected material that stays in transit did not move, so it gets no rejected entry, and transit is booked with its net stock value. This is the same fix as #66911 for the Purchase Invoice.

The same code is on version-16-hotfix and version-15-hotfix, so both backport labels are set. There the code is in `purchase_receipt.py`, so the backports may need a manual port.

### Steps to reproduce
1. Float Precision 2, perpetual inventory. Item with stock UOM Kg and UOM Box at conversion factor 0.3356, in stock at 100/Kg.
2. Submit an internal Delivery Note of 6 Box into an in-transit warehouse (2.01 Kg, value 201.00).
3. Make the inter-company Purchase Receipt: accepted qty 4, rejected qty 2, Rejected Warehouse = the in-transit warehouse. Submit it.
4. Make its return and submit it.

Before: the receipt debits transit 134.00 and credits Cost of Goods Sold 268.00. The return debits transit 402.00 and credits Cost of Goods Sold 268.00.
After: the receipt credits transit 134.00 and debits the accepted warehouse 134.00. The return reverses that. No Cost of Goods Sold entry.

<hr>This is an automatic backport of pull request #66966 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6704b1ff2944`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.