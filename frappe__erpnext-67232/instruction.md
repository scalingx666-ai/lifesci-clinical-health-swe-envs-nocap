# Issue

**Title:** fix(buying): map the rest of a source row to a purchase order in its own UOM (backport #66583)

## Description

Depends-On: #66281

Stacked on #66281: review only the commits after 466a1f4274.

With "Allow to Edit Stock UOM Qty for Purchase" on, the Supplier Quotation and Sales Order mappers worked out the qty to order from rounded stock qty: the quoted row's own stock qty, or the ordered qty that adds up the rounded stock qty of earlier Purchase Orders. Dividing that by the conversion factor gives a fraction of the row's UOM (0.99 Box instead of 1), and a whole-number UOM then fails on insert.

Fix: a shared helper adds up `qty * conversion_factor` of the submitted Purchase Order rows of each source row, converts it to the row's UOM, and the mappers take it off the row's own qty. The Material Request mapper has the same problem; it is filed as #66582. The order for the rest then over-orders the row by the rounding (2.01 Kg against 2 Kg) unless the stored ordered qty adds up qty × conversion factor too, which #66281 does.

### Steps to reproduce
1. Float precision 2. In Stock Settings, turn on "Allow to Edit Stock UOM Qty for Purchase".
2. Create a stock item with stock UOM Kg and UOM Box at conversion factor 0.333333333.
3. Submit a Supplier Quotation for 1 Box and click Create > Purchase Order: the row is for 0.99 Box (expected 1).
4. With UOM Box at 0.666666667 instead, submit a Sales Order for 3 Box, make two Purchase Orders of 1 Box from it, then Create > Purchase Order for the rest: the row is for 0.99 Box (expected 1).

<hr>This is an automatic backport of pull request #66583 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2d1c8dcc4cee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.