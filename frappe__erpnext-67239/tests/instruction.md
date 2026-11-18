# Issue

**Title:** fix(accounts): book transit with the stock value an internal purchase invoice moved (backport #66843)

## Description

**Problem:** an internal Purchase Invoice with Update Stock credits the in-transit account with `valuation_rate * stock_qty`, not with the stock value that left the in-transit warehouse. With a UOM conversion the two differ, so the in-transit account drifts from its stock value. Its return debits transit the same way.

**Fix:** book transit with the value of the invoice's transit Stock Ledger Entry, as the Purchase Receipt does, for invoices and their returns. The accepted warehouse is booked with its own stock value, and any difference goes through the existing stock adjustment entry.

### Steps to reproduce
1. Float Precision 2, perpetual inventory. Item with stock UOM Kg and UOM Box at conversion factor 0.3356, in stock at 100/Kg.
2. Submit an internal Sales Invoice with Update Stock of 6 Box at 33.56 into an in-transit warehouse (2.01 Kg, value 201.00).
3. Make the inter-company Purchase Invoice with Update Stock and submit it. Then make its return and submit it.

Before: the invoice credits transit with 201.36 (0.36 to Cost of Goods Sold), and the return debits it with 201.36. After: both book 201.00, the value of their transit stock ledger entries.
<hr>This is an automatic backport of pull request #66843 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2d1c8dcc4cee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.