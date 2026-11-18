# Issue

**Title:** fix(manufacturing): do not subtract completed qty when checking total Job Card qty

## Description

### Problem
The extra Job Card check subtracted the operation's completed qty from the total qty of its cards. Each submitted card already counts only its completed + lost qty (For Quantity - Pending Qty), so the completed qty was subtracted twice. Once an operation was complete, another card for the full qty could be saved and failed only at submit.

### Fix
Compare the total qty of the operation's cards with the allowed qty, without subtracting the completed qty.

### Test change
`test_lowered_overproduction_allowance_checks_only_job_card_operation`: the extra card for operation A is now refused when it is made ("cannot be greater than Qty To Manufacture") instead of at submit ("Completed Qty cannot be greater").

### Steps to reproduce
1. Submit a Work Order for 10 with one operation and Skip Material Transfer to WIP Warehouse on.
2. Complete the Job Card with 10 and submit it.
3. Create another Job Card for the same operation with Qty to Manufacture 10 and save it.

Expected: refused at save, as before step 2. Before: it saves and fails only at submit.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `20f2a4d16a1b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.