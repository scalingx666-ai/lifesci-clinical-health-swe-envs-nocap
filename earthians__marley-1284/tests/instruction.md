# Issue

**Title:** fix(patient): load customer_group and default_price_list in make_invoice

## Description

## Summary

Fixes the "Invoice Patient Registration" action so that the generated Sales Invoice
correctly inherits the Customer's `customer_group`, `territory`, `customer_name` and
`default_price_list`, allowing standard **Pricing Rules** (and Price Lists) to be
applied automatically at the code level.

## Problem

When a user clicks **"Invoice Patient Registration"** on a Patient record
(`Patient → invoice_patient_registration` → `make_invoice`), the resulting
Sales Invoice is created with:

- `customer_group` = the global/system default (e.g. `SEARCH Cat-1`)
- `territory` = the global/system default
- `selling_price_list` = the global default from **Selling Settings**,
  **not** the Customer's `default_price_list`

Because `frappe.new_doc("Sales Invoice")` applies defaults immediately and
`set_missing_values()` only fills **empty** fields, the wrong values are never
overwritten. As a result, any **Pricing Rule** configured with
`applicable_for = "Customer Group"` is **silently skipped** on invoices created
from the Patient registration flow.

This is reproducible whenever a Customer belongs to a non-default customer group
or has a non-default price list. Manually changing the Customer on the saved
draft triggers the client-side `customer` event, which refreshes
`customer_group` / `territory` / `selling_price_list` and then applies the
pricing rule correctly — confirming the bug is on the server-side creation path.

### Example

| Field | Customer `Mr XYZ` | Invoice (before fix) | Invoice (after fix) |
| :--- | :--- | :--- | :--- |
| `customer_group` | `SEARCH Cat-4` | `SEARCH Cat-1` ❌ | `SEARCH Cat-4` ✅ |
| `territory` | `Mumbai` | `Mumbai` | `Mumbai` |
| `selling_price_list` | `Cat-4 Selling` | global default ❌ | `Cat-4 Selling` ✅ |
| `pricing_rules` (100 % discount on `SEARCH Cat-4`) | — | `[]` ❌ | `["PRLE-0001"]` ✅ |

## Fix

In `erpnext/healthcare/doctype/patient/patient.py → make_invoice()`,
explicitly copy the required fields from the Customer **before** calling
`set_missing_values()`, so that neither Selling Settings nor any global default
can override them:

```python
sales_invoice.debit_to = get_receivable_account(company)

customer_doc = frappe.get_cached_doc("Customer", sales_invoice.customer)
sales_invoice.customer_name  = customer_doc.customer_name
sales_invoice.customer_group = customer_doc.customer_group
sales_invoice.territory      = customer_doc.territory
if customer_doc.default_price_list:
    sales_invoice.selling_price_list = customer_doc.default_price_list

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5565e66c2e86`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.