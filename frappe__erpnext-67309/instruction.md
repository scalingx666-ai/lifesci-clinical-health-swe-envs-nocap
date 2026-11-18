# Issue

**Title:** fix(stock): return only the rejected batch of an internal transfer

## Description

**Problem:** on version-15-hotfix, a return of only the rejected qty of an internal transfer Purchase Receipt for a batch item cannot be submitted:
- it has no accepted package, so building the package that puts the stock back in transit fails with "Serial and Batch Bundle None not found";
- with that guarded, it fails with "Debit and Credit not equal". The receipt valued its rejected batch package at `sales_incoming_rate`, which is per purchase UOM, while the package holds stock UOM qty. So a row in Box of 0.5 Kg posted the rejected 1.5 Kg at 75 instead of 150, and the return takes 150 back into transit but only 75 out of the rejected warehouse.

**Fix:**
- build the in-transit package from the rejected package alone when the return has no accepted package (as #67203 does on develop);
- `get_transit_rate` divides `sales_incoming_rate` by the row's conversion factor. Hand-ported from #66258 (develop, merged). Its Mergify backport #66265 still has unresolved conflicts, so it is included here; #66265 can be closed if this merges.

### Steps to reproduce
1. Perpetual inventory, an internal customer and an internal supplier for the company.
2. Batch item with stock UOM Kg and UOM Box at conversion factor 0.5. Receive 20 Kg in a source warehouse.
3. Submit an internal Delivery Note for 6 Box to an in-transit warehouse.
4. Make the inter-company Purchase Receipt with accepted qty 3 Box, rejected qty 3 Box and a rejected warehouse, and submit it.
5. Make a return against it, set accepted qty to 0 (rejected qty -3), and submit it.

Before: step 4 posts the rejected 1.5 Kg at 75, and step 5 fails ("Serial and Batch Bundle None not found", then "Debit and Credit not equal ... 75.0"). After: step 4 posts it at 150, and the return moves 1.5 Kg from the rejected warehouse back to transit at 150.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `59d77cfe0d83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.