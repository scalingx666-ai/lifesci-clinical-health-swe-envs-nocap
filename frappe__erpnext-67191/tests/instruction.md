# Issue

**Title:** fix(manufacturing): release a manufacture's finished good reservation on cancel

## Description

**Problem:** With Reserve Stock on, a Manufacture entry reserves its finished good when the Work Order belongs to a Subcontracting Inward Order. It also reserves when the entry is made from a Job Card for a semi-finished good. Cancel only released the reservation for Sales Order and Production Plan sub-assembly Work Orders. In the other two cases the reservation kept the stock, and the cancel failed with "5.0 units of Item ... needed in Warehouse ...".

**Fix:** Submit and cancel now share one check for when a Manufacture entry reserves its finished good, so cancel releases every reservation submit made.

## Summary

```diff
 StockEntry
+  skips_finished_good_reservation(pro_doc)   # Manufacture without SO, Job Card, sub-assembly or SCIO
   make_stock_reserve_for_wip_and_fg
-    inline check: SO, Job Card, sub-assembly, SCIO
+    skips_finished_good_reservation
   cancel_stock_reserve_for_wip_and_fg
-    inline check: SO, sub-assembly
+    skips_finished_good_reservation
```

## Evidence

`test_manufacture_cancel_releases_its_finished_good_reservation`
- **Before:** `ValidationError: 5.0 units of Item Basic FG Item needed in Warehouse _Test Warehouse - _TC`
- **After:** passes

The Job Card case (a semi-finished good reserved for a Work Order with Reserve Stock) failed the same way ("10.0 units of Item SFG 1 needed") and cancels after the fix.

## Merge Danger

**Door:** two-way

**Blast Radius:** narrow. Only the cancel of Manufacture entries that reserved their finished good. Submit is unchanged.

**Steps to reproduce:**
1. In Stock Settings, turn on "Enable Stock Reservation".
2. Submit a Subcontracting Inward Order for 5 and receive its raw materials.
3. Make its Work Order (Reserve Stock is on), then a Manufacture entry for 5, and submit it.
4. Cancel the Manufacture entry.

Expected: the entry cancels and its finished good reservation is cancelled. Before: "5.0 units of Item ... needed in Warehouse ...".

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `533e1355152d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.