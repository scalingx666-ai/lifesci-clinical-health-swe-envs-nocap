# Issue

**Title:** fix(selling): don't copy the inter company reference to a duplicate (backport #66991)

## Description

`inter_company_invoice_reference` on Sales Invoice and `inter_company_order_reference` on Sales Order and Purchase Order were copied to a duplicate. On submit, the duplicate repointed the counterpart document to itself, and the original lost its link. Purchase Invoice already has `no_copy` on its reference; the other three now have it too.

### Steps to reproduce
1. Submit an inter-company Sales Invoice (customer is an internal customer).
2. Make the Purchase Invoice from it and submit it.
3. Duplicate the Sales Invoice.
   - Before: the copy has Inter Company Invoice Reference set to the Purchase Invoice, and submitting it repoints the Purchase Invoice to the copy.
   - After: the field is empty on the copy.

<hr>This is an automatic backport of pull request #66991 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f487518ea283`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.