# Issue

**Title:** fix(manufacturing): do not count handed-over pending qty in the Job Card cancel check

## Description

### Problem
On cancel, the Job Card guard compares the Work Order's produced qty with completed + process loss + **pending** qty of the remaining cards. Pending qty is the part handed to another card, so counting it lets that other card be cancelled after the Work Order is fully manufactured.

### Fix
Compare the produced qty with completed + process loss only.

### Steps to reproduce
1. Create a BOM for FG with 1 RM and one operation (6 minutes). Receive RM.
2. Submit a Work Order for 10 with Skip Material Transfer to WIP Warehouse on.
3. On Job Card A, log Completed Qty 6, set Pending Qty 4 and submit.
4. From the Work Order, create a Job Card for the remaining 4, complete it with 4 and submit.
5. Submit the Manufacture entry for 10, then cancel Job Card B.

Expected: "Kindly cancel the Manufacturing Entries first". Before: the cancel is allowed and the operation drops to 6 completed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c8576d9754e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.