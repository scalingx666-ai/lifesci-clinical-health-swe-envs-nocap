# Issue

**Title:** fix(manufacturing): release a manufacture's finished good reservation on cancel (backport #67191)

## Description

Depends-On: #67191

Backport of #67191.

Extra v16 commit: `WorkOrder.cancel_reserved_qty_for_wip_and_fg` now cancels the reservations made by the stock entry, not only the ones held against the Work Order, as develop does. Without it, a finished good reserved against a Subcontracting Inward Order stays reserved. It also fixes the cancel of a Manufacture for a Sales Order-linked Work Order, which failed the same way on v16.

**Steps to reproduce:**
1. In Stock Settings, turn on "Enable Stock Reservation".
2. Submit a Subcontracting Inward Order for 5 and receive its raw materials.
3. Make its Work Order (Reserve Stock is on), then a Manufacture entry for 5, and submit it.
4. Cancel the Manufacture entry.

Expected: the entry cancels and its finished good reservation is cancelled. Before: "5.0 units of Item ... needed in Warehouse ...".

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eb2950d525f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.