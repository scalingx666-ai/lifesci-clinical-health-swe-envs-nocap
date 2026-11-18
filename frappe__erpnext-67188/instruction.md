# Issue

**Title:** fix(stock): submit an internal receipt whose rejected stock qty rounds to 0 (backport #66996)

## Description

An internal receipt row whose rejected qty rounds to 0 in the stock UOM posts no rejected Stock Ledger Entry. Submit then failed:
- `get_stock_value_difference` returned `None` for the missing entry, and `make_divisional_loss_gl_entry` subtracted it (`TypeError`). It now returns 0, which also covers its other two callers.
- For a batch item the row was still treated as rejecting stock, so a rejected package was made with qty 0, which `make_package_for_transfer` turns into the full delivered qty. The internal receipt checks now go through `has_rejected_stock`, which looks at the rejected stock qty, so such a row is handled like a row that rejects nothing.

The test extends `make_transfer_receipt` with an optional UOM for the Delivery Note; existing callers are unchanged.

This touches `set_rejected_package` and the internal receipt checks that #66969 and #66973 also change, so whichever merges later needs a rebase. With #66969, `has_rejected_stock` should use its `get_rejected_stock_qty`.

### Steps to reproduce
1. System Settings: Float Precision 2. Perpetual inventory, an internal customer and an internal supplier for the company.
2. Item with stock UOM Kg and a UOM Gram at conversion factor 0.001. Receive 20 Kg in a source warehouse.
3. Submit an internal Delivery Note for 1000 Gram to an in-transit warehouse.
4. Make the inter-company Purchase Receipt from it with accepted qty 999, rejected qty 1 and a rejected warehouse, and submit it.
   - Before: `TypeError` in `make_divisional_loss_gl_entry`; for a batch item, "Total quantity 1.00 in the Serial and Batch Bundle ... does not match with the quantity 0.00".
   - After: it submits and posts no rejected stock.

<hr>This is an automatic backport of pull request #66996 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b0de778a836`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.