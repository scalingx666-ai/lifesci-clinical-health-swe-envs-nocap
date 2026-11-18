# Issue

**Title:** fix(manufacturing): set Material Requested only when a plan row was requested

## Description

### Problem
`update_requested_status` set Material Requested when every raw material row had `requested_qty >= quantity`. A row with quantity 0 always passes, so a plan whose raw materials are all in stock became Material Requested on submit with no Material Request.

### Fix
Ignore rows with quantity 0, and set Material Requested only when at least one row needs a request.

### Steps to reproduce
1. Create RM and FG with BOM FG = RM × 1. Receive 100 RM into Stores.
2. Create a Production Plan for 10 FG with For Warehouse = Stores and get the raw materials (Required Qty 0).
3. Submit the plan.

Expected: status Submitted (Not Started). Before: Material Requested.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4f675270770`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.