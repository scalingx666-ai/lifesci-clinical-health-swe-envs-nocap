# Issue

**Title:** fix(stock): a draft can't take over the serial and batch bundle of another draft (backport #66994)

## Description

A draft transaction could link the Serial and Batch Bundle of another draft. On save, `set_serial_and_batch_values` repointed the bundle's voucher to the new row, while the first draft still linked it, so later changes on one draft changed the bundle the other uses. The bundle now refuses to move while its own voucher is a different draft. Bundles of submitted, cancelled or not yet saved vouchers are not affected, so the flows that hand over a submitted voucher's bundle (POS consolidation, pick lists) keep working.

### Steps to reproduce
1. Make two draft Purchase Receipts A and B for a batch item, each with its own Serial and Batch Bundle on the row.
2. On B, set the row's Serial and Batch Bundle to A's bundle and save B.
   - Before: B saves and the bundle now points to B, while A still links it.
   - After: "Row #1: Serial and Batch Bundle ... belongs to Purchase Receipt A. Select or create another bundle."

<hr>This is an automatic backport of pull request #66994 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b0de778a836`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.