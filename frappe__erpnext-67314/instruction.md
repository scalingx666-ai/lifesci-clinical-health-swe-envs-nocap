# Issue

**Title:** fix(stock): take no more out of transit than an internal delivery row left there (backport #66746)

## Description

Depends-On: #66794
Depends-On: #66692

Stacked on #66692: review only the commits after 2b63f16104.

**Problem:** Each partial receipt of an internal Delivery Note converts and rounds its own qty, and takes that out of the in-transit warehouse. When the parts round up, the receipts together take more than the delivery put there, and the last one fails with a negative stock error.

**Fix:** An internal Purchase Receipt takes no more out of transit than its delivered row left there, after its other receipts and their returns. A return of the receipt puts back no more than the receipt took. On cancel, a row reverses what its own transit entry posted. Only rounding is capped: an over-receipt, a row with a serial or batch package, and a cap with nothing left keep their own stock qty, as before.

Known limits: two rows of one receipt (or return) against the same row still round on their own. The accepted warehouse still gets the row's own rounded stock qty (1.01 Kg against 1.00 Kg out of transit below), so the 0.01 Kg value difference is booked to Cost of Goods Sold, as in #66692. Purchase Invoices with Update Stock are #66754.

**Steps to reproduce:**
1. Float Precision 2. Item with stock UOM Kg and UOM Box at conversion factor 0.3356, in stock in the source warehouse.
2. Submit an internal Delivery Note of 6 Box to an in-transit warehouse. The transit warehouse gets 2.01 Kg.
3. Make an inter-company Purchase Receipt for 3 Box and submit it. It takes 1.01 Kg out of transit.
4. Make a second inter-company Purchase Receipt for the other 3 Box and submit it.

Expected: the second receipt takes the 1.00 Kg left in transit. Before: it takes 1.01 Kg and fails with a negative stock error for 0.01 Kg.

<hr>This is an automatic backport of pull request #66746 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `118532ea8363`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.