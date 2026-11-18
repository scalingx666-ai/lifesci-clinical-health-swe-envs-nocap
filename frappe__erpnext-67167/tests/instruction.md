# Issue

**Title:** fix(selling): no second inter company sales invoice from a purchase invoice (backport #66993)

## Description

The inter-company Sales Invoice mapper has no received qty for a Purchase Invoice source, so it mapped the full qty every time. Through the API, a second Sales Invoice could be made for a Purchase Invoice that already had one, and its submit repointed the Purchase Invoice to the duplicate. Purchase Invoice rows link no Sales Invoice rows, so the mapper now refuses a Purchase Invoice whose Inter Company Invoice Reference is already set.

### Steps to reproduce
1. Submit an inter-company Purchase Invoice (internal supplier) for 10 units.
2. Make the Sales Invoice from it and submit it.
3. Call `erpnext.accounts.doctype.purchase_invoice.mapper.make_inter_company_sales_invoice` with the same Purchase Invoice.
   - Before: a new Sales Invoice for all 10 units is mapped.
   - After: "Cannot create Intercompany Sales Invoice. Purchase Invoice ... already has Sales Invoice ...".

<hr>This is an automatic backport of pull request #66993 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d51242938426`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.