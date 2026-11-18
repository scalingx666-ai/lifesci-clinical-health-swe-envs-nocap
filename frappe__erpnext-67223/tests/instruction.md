# Issue

**Title:** fix: don't add default taxes to a return of a document with no taxes (backport #66912)

## Description

## Problem
A return made from a document with no taxes gets the company's default tax template. The `company` trigger runs on load of every new document, including a mapped return, and calls `apply_default_taxes()`, which fills the empty taxes table with the default template. The credit note then reverses tax that the invoice never charged.

## Fix
`apply_default_taxes()` does nothing for a return made against a document, same as `update_item_tax_map()`. The return keeps the taxes of its source. Other mapped documents (for example Purchase Order from Material Request) and new documents still get the default template. The server side does not add default taxes to a return, so it needs no change.

## Steps to reproduce
1. Set a default Sales Taxes and Charges Template for the company (for example "US ST 6%", Is Default checked).
2. Create a Sales Invoice with one item, qty 2, rate 100. Clear the template and the Taxes table. Save and submit. Grand Total is 200.
3. Click Create > Return / Credit Note.

Before: the credit note gets "US ST 6%" and Grand Total is -212.
After: the credit note has no taxes and Grand Total is -200.

The same applies to a Purchase Receipt return of a receipt with no taxes.

<hr>This is an automatic backport of pull request #66912 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fdc3dbc37273`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.