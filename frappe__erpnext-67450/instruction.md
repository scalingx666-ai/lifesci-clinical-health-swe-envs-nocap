# Issue

**Title:** fix(manufacturing): reserve nothing for a row consumed past its required qty

## Description

**Problem:** with Skip Material Transfer to WIP, a Work Order row's share of Reserved Qty for Production is `required_qty - consumed_qty` with no floor. A Work Order that consumed 12 of the 10 it needs adds -2 and lowers the reservation of other Work Orders.

**Fix:** a row consumed past its required qty reserves 0, as the transfer branch already does for `transferred_qty`.

### Steps to reproduce
1. Receive 40 of a raw material. BOM: 1 finished good uses 1 raw material.
2. Submit Work Order 1 for 10 and Work Order 2 for 5, both with Skip Material Transfer to WIP (reserved for production 15).
3. Manufacture 5 on Work Order 1, consuming 12 of the raw material.

Before: Reserved Qty for Production 3. After: 5.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c8576d9754e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.