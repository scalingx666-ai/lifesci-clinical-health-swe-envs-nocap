# Issue

**Title:** fix(stock): reserve a fractional stock qty in full across batches (backport #66965)

## Description

**Problem:** When a stock reservation takes more than one batch, the qty left to reserve after each batch is rounded to the float precision. With a fractional stock qty (1 Box = 0.33333 Kg), the last batch gets 0.133 Kg instead of 0.13333 Kg. The reservation stays "Partially Reserved", and the Delivery Note made from it gets 0.999 Box, which fails on a whole-number UOM. A single-batch reservation already reserves the full 0.33333 Kg.

**Fix:** Keep the unrounded qty left to pick in `get_qty_based_available_batches`, and round it only to check if more is needed.

The same code is on version-16-hotfix and version-15-hotfix.

### Steps to reproduce

1. Set float precision to 3. In Stock Settings, turn on "Enable Stock Reservation" and "Auto Reserve Serial and Batch Nos", and turn off "Use Serial / Batch Fields".
2. Make a batched item (auto-create batches) with stock UOM Kg and UOM Box (Must be Whole Number) = 0.33333 Kg.
3. Receive 0.2 Kg twice with two Material Receipts (two batches).
4. Submit a Sales Order for 1 Box and reserve its stock.
5. Make a Delivery Note for the reserved stock and submit it.

Before: the reservation is 0.333 Kg ("Partially Reserved"). The Delivery Note gets 0.999 Box and fails with "Quantity (0.999) cannot be a fraction".
After: the reservation is 0.33333 Kg ("Reserved"). The Delivery Note gets 1 Box and submits, and the reservation becomes "Delivered".

<hr>This is an automatic backport of pull request #66965 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b0de778a836`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.