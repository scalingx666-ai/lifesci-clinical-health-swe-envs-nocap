# Issue

**Title:** refactor: split early payment discount without a Payment Entry (backport #66981)

## Description

## Problem

The functions that split an early payment discount into a loss on income and a loss on taxes need a **Payment Entry** document. Code that books the same discount in a different document, for example a **Journal Entry**, cannot call them directly.

## Solution

The calculation is now in one function that does not need a **Payment Entry**:

```python
rows, base_total_discount_loss = get_early_payment_discount_loss(
	doc, valid_discounts, payment_type, company, cost_center=None
)
```

- `rows` is a list of `account`, `cost_center` and `amount`. Amounts are negative for payment type "Pay".
- `base_total_discount_loss` is the total loss before the rows are rounded. The caller needs it to calculate the remaining rounding loss.
- If `cost_center` is empty, the function uses the default cost center of the company.

`split_early_payment_discount_loss(pe, doc, valid_discounts)` keeps its signature. It calls the new function and appends the rows to `deductions`. The behavior of **Payment Entry** does not change.

## Removed functions

`add_income_discount_loss` and `add_tax_discount_loss` are removed. Their logic is now in `get_early_payment_discount_loss`. Apps that call them directly must change to the new function.

## Tests

- Added `test_early_payment_discount_loss_without_payment_entry`, which calls the new function with an unsubmitted **Sales Invoice** and no **Payment Entry**.
- The existing **Payment Entry** tests for early payment discounts pass without changes.<hr>This is an automatic backport of pull request #66981 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1db3629679fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.