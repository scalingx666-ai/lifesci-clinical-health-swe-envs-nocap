# Issue

**Title:** fix(accounts): no inter-company purchase invoice from a sales invoice made from one (backport #66968)

## Description

**Problem:** a Sales Invoice made from an inter-company Purchase Invoice links that Purchase Invoice in `inter_company_invoice_reference`, but the Purchase Invoice rows have no `sales_invoice_item`. So `get_received_items` returns nothing, and `make_inter_company_purchase_invoice` maps the full qty again. The same happens for a Purchase Order made from a Sales Order that was made from a Purchase Order, and the other way round.

**Fix:** when the source links its counterpart but no counterpart row links back to a source row, the mapper stops with an error. This is the server side of the check the form already does (#66937).

The same code is on version-16-hotfix and version-15-hotfix, so both backport labels are set.

### Steps to reproduce
1. Submit an inter-company Purchase Invoice for 10 units (supplier is an internal supplier that represents another company).
2. Make the Sales Invoice from it and submit it.
3. Call `erpnext.accounts.doctype.sales_invoice.mapper.make_inter_company_purchase_invoice` with that Sales Invoice.

Before: a new Purchase Invoice for all 10 units is mapped. After: "Cannot create Intercompany Purchase Invoice. Sales Invoice ... was created from Purchase Invoice ...". A Purchase Invoice made from a normal internal Sales Invoice still maps the pending qty.

<hr>This is an automatic backport of pull request #66968 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f487518ea283`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.