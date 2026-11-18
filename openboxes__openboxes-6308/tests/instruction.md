# Issue

**Title:** Fix the running balance in the transaction report details dialog

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** #6201

**Description:**

Part of #6201. When you click a row of the transaction report, the details dialog lists the product's transactions over the period with a running balance. For some products, the running balance didn't end at the closing balance, so the dialog looked wrong even when the report was right.

**Cause:** the running balance skipped product inventory transactions (inventory baselines and older product inventory counts). Quantity on hand is set to the quantity of those transactions, not added to it. When a count's quantity differed from the balance before it, the dialog carried the old balance forward instead.

A count can differ from the transactions before it, even with no adjustment, because a baseline preserves quantity on hand. If a transaction dated before the count is deleted or entered later (for example, a shipment is rolled back), quantity on hand doesn't change. In a production copy, about 2% of the products at a large depot had a running balance that didn't match its closing balance over 8 months, all for this reason.

**Changes** (`ReportService.getTransactionReportModalData`)

- At a product inventory transaction, the running balance is set to the quantity of its entries. A count with several entries (e.g. one per lot or bin) adds up its entries, so the last one shows the counted total.
- Transactions are sorted by transaction date, then by date created, which is the order quantity on hand is calculated in. Before, transactions with the same transaction date could be in any order, so a count and a movement at the same time could be shown the wrong way around.

The dialog itself doesn't change.

#### How to test

1. Find a product whose running balance in the dialog didn't end at the closing balance before this change, for example a product that was counted and then had an earlier transaction deleted.
2. Open the dialog. At each count, the balance should be the counted quantity, and the last balance should equal the closing balance.
3. For a product without counts in the period, the dialog should be unchanged.

Integration tests: `ReportServiceTransactionReportModalDataSpec`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RqDhKQyrN4ZX1iZUg4RvAm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a19378538056`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.