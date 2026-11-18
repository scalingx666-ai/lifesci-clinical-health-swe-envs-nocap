# Issue

**Title:** fix(buying): don't delete a purchase order row an inter company sales order links (backport #66992)

## Description

Update Items on a Purchase Order deleted a row that an inter-company Sales Order row links through `purchase_order_item`. The Sales Order row, and the documents made from it, kept a link to a row that no longer exists. Deleting such a row now throws, naming the Sales Order.

### Steps to reproduce
1. Submit an internal Purchase Order (internal supplier) with two rows, A and B.
2. Make the inter-company Sales Order from it with row A only and submit it.
3. On the Purchase Order, Update Items and remove row A.
   - Before: row A is deleted and the Sales Order row still points to it.
   - After: "Row #1: Cannot delete item ... which is already ordered on Sales Order ...".

<hr>This is an automatic backport of pull request #66992 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b0de778a836`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.