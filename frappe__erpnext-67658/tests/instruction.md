# Issue

**Title:** fix(selling): reserve nothing for a row delivered again after a return (backport #67445)

## Description

**Problem:** with "Don't reserve Sales Order qty on sales return" on, a row's reserved share is `qty - delivered_qty - returned_qty`. `delivered_qty` is already net of returns, so after a replacement delivery the share is negative (10 - 10 - 4 = -4), and the Bin sum takes it off the reservation of other Sales Orders.

**Fix:** floor the row's share at 0.

### Steps to reproduce
1. Selling Settings: turn on "Don't reserve Sales Order qty on sales return". Receive 100 of an item.
2. Submit Sales Order A for 5 and Sales Order B for 10.
3. Deliver all 10 of B, return 4 of that delivery, then deliver the 4 again from B.

Before: Reserved Qty 1. After: Reserved Qty 5 (Sales Order A only).
<hr>This is an automatic backport of pull request #67445 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06107678248e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.