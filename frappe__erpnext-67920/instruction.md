# Issue

**Title:** fix(manufacturing): list only Sales Orders with a BOM item in a Production Plan (backport #67487)

## Description

Get Sales Orders on a Production Plan listed every open Sales Order when Item Code was empty, even orders with no item that has a BOM. The BOM subquery was tied to the order item only when Item Code was set, so it matched any active BOM in the system.

Fix: always match a BOM of the order item (or of its template, as Get Finished Goods uses the template BOM for a variant). Same change in Get Finished Goods (`_so_items`).

Steps to reproduce:
1. Create a stock item TRADE with no BOM (other items in the company have active BOMs).
2. Submit a Sales Order for 5 TRADE.
3. Create a Production Plan, Get Items From = Sales Order, Customer = the order's customer, Item Code empty. Click Get Sales Orders.
4. Before: the order is listed and Get Finished Goods adds nothing. After: the order is not listed.

<hr>This is an automatic backport of pull request #67487 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b3cbafb9db0c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.