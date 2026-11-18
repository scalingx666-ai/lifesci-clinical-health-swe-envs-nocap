# Issue

**Title:** fix(manufacturing): offer the stock UOM qty in the Production Plan reserve dialog

## Description

### Problem
The Reserve for Raw Materials dialog divided the unreserved qty by the row's Conversion Factor. On Production Plan rows that is the purchase UOM factor, but Reqd Qty (BOM) and Stock Reserved Qty are both in stock UOM, and the server reserves the dialog qty as stock qty. A need of 135 Kg (Box = 12 Kg) was offered and reserved as 11.25 Kg.

### Fix
Do not divide the dialog qty by the conversion factor. Every qty field the dialog reads and sends back (Production Plan and Work Order) is in stock UOM.

### Steps to reproduce
1. Turn on Enable Stock Reservation. Create RM (stock UOM Kg, Purchase UOM Box = 12 Kg) and FG with BOM FG = RM × 13.5.
2. Submit a Production Plan for 10 FG with Reserve Stock on while there is no RM in stock (one raw material row, Reqd Qty (BOM) 135).
3. Receive 200 Kg RM and click Reserve for Raw Materials.

Expected: the dialog offers 135 and 135 Kg is reserved. Before: 11.25.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4f675270770`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.