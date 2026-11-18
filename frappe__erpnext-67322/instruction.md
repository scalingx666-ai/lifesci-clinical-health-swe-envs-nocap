# Issue

**Title:** fix(selling): don't delete a sales order row a draft purchase order links (backport #67156)

## Description

Update Items on a Sales Order deletes a row that a draft Purchase Order row links through `sales_order_item`. The `ordered_qty` check in `validate_child_on_delete` counts only submitted Purchase Orders, so the draft keeps a link to a row that no longer exists.

Fix: refuse to delete a Sales Order row that a draft or submitted Purchase Order row links. It shares one helper with the Purchase Order side added in #66992.

### Steps to reproduce
1. Submit a Sales Order with two rows, A and B.
2. Make a Purchase Order from it with row A only, and save it as draft.
3. On the Sales Order, Update Items and remove row A: it is deleted, and the draft Purchase Order row still links it.

<hr>This is an automatic backport of pull request #67156 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8ed342331912`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.