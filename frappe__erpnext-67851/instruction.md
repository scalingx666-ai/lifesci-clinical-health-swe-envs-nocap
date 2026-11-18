# Issue

**Title:** fix(manufacturing): compare a Manufacture request's ordered qty with its stock qty (backport #67480)

## Description

### Problem
For a Manufacture Material Request, the item's Ordered Qty is the Work Order qty in stock UOM. The plan subtracted it from `qty` (request UOM). For 2 Box (24 Kg), a Work Order of 12 Kg made 2 - 12 negative, so the request was no longer listed and Get Finished Goods got nothing.

### Fix
Compare Ordered Qty with the request row's `stock_qty`, in the pending qty and in both filters.

### Steps to reproduce
1. Create FG with stock UOM Kg, UOM Box = 12 Kg, and a BOM.
2. Submit a Material Request (Purpose Manufacture) for 2 Box FG.
3. Submit a Work Order for 12 Kg FG against this request.
4. Create a Production Plan, click Get Material Request, then Get Finished Goods.

Expected: the request is listed and 12 Kg is pulled. Before: it is not listed and nothing is pulled.

<hr>This is an automatic backport of pull request #67480 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3eed198a65e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.