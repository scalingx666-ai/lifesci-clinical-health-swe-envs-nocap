# Issue

**Title:** fix(subcontracting): reopen only a cancelled transfer's own reservation

## Description

**Problem:** When a Subcontracting Order row has more than one reservation, cancelling a Send to Subcontractor entry takes the qty back from the first reservation that matches its batch, not from the one that transfer used. Reserve 6 of batch A, then 4 more of batch A. Transfer 6 and then 4, and cancel the second transfer. The reservations end at Transferred Qty 2 and 4 instead of 6 and 0.

The cancel also fails first: the transfer's own reservation in the supplier warehouse still holds the stock that the cancel takes out.

**Fix:**
- Cancel the transfer's supplier warehouse reservations before its stock ledger entries are reversed.
- On cancel, rebuild the transferred qty of the row's reservations from the remaining submitted transfers, as Work Orders already do. One query reads the remaining transfers and their batches for the whole entry.

## Summary

```diff
 StockEntry.on_cancel
+  cancel_stock_reservation_entries_for_subcontracting   # supplier warehouse SREs made by this transfer
   update_stock_ledger
   update_stock_reservation_entries
-    reverse this transfer's qty, first matching reservation first
+    rebuild_subcontracting_transfers
+      remaining transfers' qty, serial nos and batch qty per sco_rm_detail
+      fill each reservation again in the same order as a submit
```

## Evidence

`test_transfer_cancel_reopens_the_reservations_of_the_remaining_transfers`
- **Before:** `((6.0, 2.0), (4.0, 4.0)) != [(6, 6), (4, 0)]`
- **After:** passes

## Merge Danger

**Door:** two-way

**Blast Radius:** narrow. Only the cancel of a Send to Subcontractor entry whose Subcontracting Order reserves stock. Submit is unchanged.

**Steps to reproduce:**
1. In Stock Settings, turn on "Enable Stock Reservation", "Auto Reserve Serial and Batch" and "Allow Partial Reservation".
2. Create a batched raw material and a subcontracted item whose BOM uses 1 of it. Receive 6 of the raw material in batch A.
3. Submit a Subcontracting Order for 10 with Reserve Stock on. It reserves 6 of batch A.
4. Receive 4 more of batch A and click Reserve on the order. It reserves 4 of batch A.
5. Make a Stock Entry (Send to Subcontractor) for 6 of batch A and submit it. Then make one for 4 of batch A, submit it and cancel it.

Expected: the cancel goes through and the reservations show Transferred Qty 6 and 0. Before: the cancel fails with a negative stock error in the supplier warehouse. After you cancel that transfer's supplier warehouse reservation by hand, the reservations show 2 and 4.

Supersedes #67169

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8542f2a9e126`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.