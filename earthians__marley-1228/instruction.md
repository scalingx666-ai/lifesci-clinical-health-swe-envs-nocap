# Issue

**Title:** fix(sales-invoice): serialize prescription row inserts to avoid rate race

## Description

Fixes a race condition in **Get Items from Prescriptions** (Sales Invoice → Get Items From → Prescriptions) where selecting 3 or more drug rows at once could leave some rows - typically the ones in the middle - with no rate, even though every item has a valid price.

Reported here: https://discuss.frappe.io/t/marley-healthcare-get-items-from-prescriptions-problem/164817

## Fix

Made `add_to_item_line()` async and `await` each `frappe.model.set_value` call in the drug-rows loop, so a row's `item_code` change (and its rate fetch) fully resolves before the next row is added. This serializes the work instead of racing it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ef83ab2b3ed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.