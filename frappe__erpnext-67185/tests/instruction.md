# Issue

**Title:** fix(selling): show inter company order button while order qty is pending (backport #66964)

## Description

**Problem:** the Sales Order form adds Create > Internal (or Inter Company) Purchase Order only when `inter_company_order_reference` is empty. The Purchase Order form does the same for Create > Internal (or Inter Company) Sales Order. That field is set as soon as one counterpart order is submitted, so the button stays hidden while qty is still pending (after a partial order). The server mapper supports partial orders in both directions.

**Fix:** drop that condition and add the button only after a pending-qty check through `get_received_items`, in the row's UOM and rounded to `qty` precision, as the mapper does. Closed rows do not count, as the mapper skips them. An order made from its counterpart links it without item references, so the button stays hidden there. The check is one shared method on the transaction controller, used by both forms. It also checks create permission on the target doctype, which the Purchase Order form did not. It is the same as the Sales Invoice fix in #66937. The server mapper blocks fully ordered qty.

The same condition is on version-16-hotfix and version-15-hotfix, so both backport labels are set. On those branches `get_received_items` is in `sales_invoice.py`, so the backports need the method path changed.

### Steps to reproduce
1. Submit an internal Sales Order for 2 units (customer is an internal customer).
2. Make an internal Purchase Order from it for 1 unit and submit it.
3. Reload the Sales Order.

Before: Create > Internal Purchase Order is hidden. After: it is shown for the 1 pending unit, and hidden again once that unit is ordered. The same applies to a Purchase Order and Create > Internal Sales Order.

<hr>This is an automatic backport of pull request #66964 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b0de778a836`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.