# Issue

**Title:** fix(selling): show the internal purchase invoice button while sales invoice qty is pending (backport #66937)

## Description

**Problem:** the Sales Invoice form adds Create > Internal (or Inter Company) Purchase Invoice only when `inter_company_invoice_reference` is empty. That field is set as soon as one Purchase Invoice is submitted against the Sales Invoice, so the button stays hidden while qty is still pending (after a partial Purchase Invoice).

**Fix:** drop that condition and add the button only after its pending-qty check through `get_received_items`, rounded to `stock_qty` precision. A Sales Invoice made from a Purchase Invoice links it without item references, so the button stays hidden there. The server mapper checks the pending qty too.

The same condition is on version-16-hotfix and version-15-hotfix, so both backport labels are set.

### Steps to reproduce
1. Submit an internal Sales Invoice for 2 units (customer is an internal customer).
2. Make an internal Purchase Invoice from it for 1 unit and submit it.
3. Reload the Sales Invoice.

Before: Create > Internal Purchase Invoice is hidden. After: it is shown for the 1 pending unit, and hidden again once that unit is invoiced.

<hr>This is an automatic backport of pull request #66937 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `89f13f3695b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.