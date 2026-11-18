# Issue

**Title:** fix(Sample Collection): fetch reference_doc when linking sales invoice to observation (backport #1062)

## Description

## Summary

PR #555 added a conditional check so `sales_invoice` is only set when the Sample Collection comes from a Sales Invoice. However, `insert_observation()` never fetches `reference_doc` from the database, so the condition is always false and `sales_invoice` stays NULL after Mark Collected. This resulted in Diagnostic report not having "Result entry" UI for the observations within it.

## Fix
Add `reference_doc` to the `frappe.db.get_value()` field list in `insert_observation()`.

## Test plan
- [ ] Create Sales Invoice with a lab test that requires sample collection
- [ ] Submit invoice → Sample Collection created with `reference_doc = Sales Invoice`
- [ ] Mark Collected
- [ ] Confirm Observation has `sales_invoice` set to the invoice name
- [ ] Open Diagnostic Report → result entry widgets load
- [ ] Confirm encounter-based sample collections still get `sales_invoice = NULL` (no invalid invoice reference)<hr>This is an automatic backport of pull request #1062 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c76c0b3d936a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.