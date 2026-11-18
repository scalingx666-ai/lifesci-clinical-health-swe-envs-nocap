# Issue

**Title:** fix(buying): count returns of internal purchase invoices as uninvoiced (backport #66916)

## Description

Backport of #66916. Hand-ported: on version-15-hotfix the code is in `stock_controller.py` and `sales_invoice.py`, not `internal_transfer.py` and `mapper.py`.

### Steps to reproduce
1. Submit an internal Sales Invoice with Update Stock for 6 units to an in-transit warehouse.
2. Make the internal Purchase Invoice with Update Stock and submit it.
3. Make its return with Update Stock and submit it. The 6 units go back to transit.
4. Call `make_inter_company_purchase_invoice` for the Sales Invoice again and submit the result.

Before: "Cannot create Intercompany Purchase Invoice. All items in the source Sales Invoice have already been fully invoiced." After: a Purchase Invoice for 6 units, which takes the 6 units out of transit. A third one is blocked again. Cancelling the return from step 3 is then blocked.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06107678248e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.