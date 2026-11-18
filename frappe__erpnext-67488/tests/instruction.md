# Issue

**Title:** fix(manufacturing): count stock to be transferred once in Production Plan required materials

## Description

Download Required Materials without a For Warehouse counted the stock of the selected Warehouses twice. With no For Warehouse and no default warehouse, the shortage was sized on the stock of all warehouses (selected ones included), and the transfer step then took the same stock from the selected Warehouses again.

Fix: when the plan transfers from the selected Warehouses, leave their stock out of the shortage. The group-warehouse case keeps its For Warehouse-only shortage. The Projected Qty column still shows the stock of the whole scope, as it does for a group warehouse.

Steps to reproduce:
1. Item RM (Kg), item FG with a BOM: FG = RM × 2.
2. Receive 7 RM into Stores and 5 RM into Work In Progress.
3. Production Plan for 10 FG, For Warehouse empty, save.
4. Raw Material tab > Download Required Materials, Warehouses = Work In Progress.
5. Before: Required Qty 8 (5 transfer + 3 buy), so 15 Kg for a need of 20. After: Required Qty 13 (5 transfer + 8 buy).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4f675270770`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.