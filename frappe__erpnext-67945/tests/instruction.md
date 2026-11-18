# Issue

**Title:** fix(selling): link only a Selling Blanket Order of the customer on a Quotation (backport #67492)

## Description

On a Quotation, the Blanket Order link offered only Purchasing Blanket Orders, the item lookup picked any Blanket Order for the item whatever its type or customer, and a Quotation saved with a Purchasing or another customer's Blanket Order.

Fix:
- The link query asks for Selling Blanket Orders on a Quotation and offers only the party's orders.
- The lookup filters the Blanket Order type and the party. A Quotation to a Lead or Prospect uses the Customer made from it.
- A Quotation runs the same Blanket Order checks as a Sales Order (open, not expired, type, party, currency, closed rows), except the qty check, since a Quotation orders nothing.

Steps to reproduce:
1. Item FG. Submit a Purchasing Blanket Order (Rate 40, To Date in 3 days), a Selling one for Customer A (60, 5 days) and one for Customer B (90, 30 days).
2. Quotation for Customer B, add FG with Against Blanket Order on.
3. Before: it picks the Purchasing order at 40; saving with it works. After: it picks Customer B's order at 90; saving with the Purchasing or Customer A's order fails.

Overlap: open #65285 also changes `validate_order_matches` and `_get_blanket_order_details`.

<hr>This is an automatic backport of pull request #67492 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e7709a921cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.