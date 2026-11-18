# Issue

**Title:** fix(accounts): validate invoice and payment limits in payment reconciliation

## Description

## Summary

Fixes an issue in Payment Reconciliation where setting **Invoice Limit** to a negative value causes an unhandled SQL syntax error and results in an HTTP 500 Server Error.

## Issue Description

In Payment Reconciliation, entering a negative value in the **Invoice Limit** field causes an SQL syntax error when fetching unreconciled invoice entries.

Although PR #66304 introduced `validate_payment_limit()` to validate `payment_limit`, the validation was not extended to `invoice_limit`.

When a negative value is entered, `get_invoice_entries()` passes `self.invoice_limit` to `get_outstanding_invoices()`. This value is eventually used by `QueryPaymentLedger.query_for_outstanding()`, where `.limit(-5)` is compiled into raw SQL as `LIMIT -5`.

MariaDB does not support negative values in the SQL `LIMIT` clause, resulting in the following error:

```text
MySQLdb.ProgrammingError: (1064, "You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near '-5' at line 1")
```

This causes an uncaught HTTP 500 error and displays a Server Error modal in Desk.

The **Invoice Limit** field description specifies that a value of zero should fetch all entries. Negative values should therefore be validated or handled without generating invalid SQL.

## Steps to Replicate

1. Navigate to **Payment Reconciliation** using the Awesomebar or the following URL:
   `/desk/accounts/payment-reconciliation/Payment%20Reconciliation`
2. Set **Company** to `_Test Company`.
3. Set **Party Type** to `Customer`.
4. Select **Party** as `_Test Customer B`.
5. Set **Receivable/Payable Account** to `Debtors - _TC`.
6. Enter `-5` in the **Invoice Limit** field.
7. Click **Get Unreconciled Entries**.

## Actual Behavior

- A **Server Error** modal appears in Desk.
- The error reports `MySQLdb.ProgrammingError: 1064` due to the invalid SQL `LIMIT -5` clause.
- The `/api/method/run_doc_method` request fails with HTTP 500.

## Expected Behavior

- Negative values in **Invoice Limit** should be validated and prevented from reaching the SQL query.
- A value of `0` should continue to fetch all entries, as specified in the field description.
- The system should handle invalid limit values gracefully without producing an SQL syntax error or HTTP 500 response.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f6c7d5b1db85`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.