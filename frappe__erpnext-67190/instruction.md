# Issue

**Title:** fix(stock): value an internal transfer receipt at the stock qty that leaves transit (backport #66943)

## Description

**Problem:** an internal transfer receipt row is valued at `qty × sales_incoming_rate`, which is the value of the unrounded stock qty, divided by the rounded stock qty. With a UOM conversion the valuation rate is off (100.179 instead of 100 per Kg). A non-batch row is re-anchored to the Delivery Note rate in the stock ledger, but a batch row keeps the bundle rate, so the target warehouse takes more value than leaves transit and the difference posts to Cost of Goods Sold. A back-dated receipt hides it, because its repost revalues the row.

**Fix:** value the row at the rounded stock qty that leaves transit times the transit rate per stock UOM (`sales_incoming_rate / conversion_factor`, as `get_transit_rate` in the bundle already does). A stock updating internal Purchase Invoice return takes back the same value, so it does not post a one-sided stock adjustment and fail.

The same line is on version-16-hotfix and version-15-hotfix, so both backport labels are set. With rejected qty, a separate qty rounding gap is left (#66941).

### Steps to reproduce
1. System Settings: Float Precision 2. Internal customer and internal supplier for the company.
2. Batch item (stock UOM Kg, UOM Box at conversion factor 0.3356, create new batch on). Receive 20 Kg at rate 100.
3. Submit an internal Delivery Note for 4 Box to an in-transit warehouse (1.34 Kg at 134.00).
4. Create the inter-company Purchase Receipt from it, set the target warehouse and posting time after the Delivery Note, and submit.

Before: the target warehouse posts +134.24 and the receipt books Stock In Hand Dr 0.24 / Cost of Goods Sold Cr 0.24. After: +134.00 and no GL entry.

<hr>This is an automatic backport of pull request #66943 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b0de778a836`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.