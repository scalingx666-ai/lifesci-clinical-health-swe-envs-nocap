# Issue

**Title:** Calculate transaction report credits and debits in the database

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** #6201

**Stacked on #6263 (phase 1). Please review that PR first.** This PR's base is the phase 1 branch, so the diff only shows the phase 2 changes.

**Description:**

This is the second part of the fix for #6201, where the transaction report can run the server out of memory.

After phase 1, the opening and closing balances are calculated in the database. But the report still loaded every credit and debit `TransactionEntry` in the date range as a full Hibernate entity: about 28k per request for a large facility, plus Hibernate's bookkeeping for each one. It then matched balances to products with an O(n²) loop (`AvailableItemMap.getAllByProduct` once per product). In a burst of concurrent requests, those entities filled the old generation and caused continuous full GCs.

This PR changes how the totals are calculated:

- **`getTransactionReportTotals`** (new) sums the credits and debits per product and transaction type in a single SQL aggregate. It also calculates the per-type quantities and backdated corrections for the CSV. Only the matching products are loaded, not the transaction entries.
- **Balances are grouped by product once** (`sumQuantityOnHandByProduct`) instead of being scanned once per product.
- **`getTransactionReport` runs in a read-only transaction.**

The summary view and the CSV both use this. The single-product details dialog is unchanged.

#### Same results

The definitions are unchanged:

- **Credits:** positive quantities of CREDIT transactions.
- **Debits:** DEBIT quantities, plus negative quantities of CREDIT transactions.
- **Period:** after the start date and before the end date.
- **Included products:** only those with a credit or debit in the period.

The filters (category, tag, catalog, product) behave as before, except for the tag fix below.

Checked against real data: the CSV for a large facility over 8 months (1,753 products, 19 columns) is **identical** to the one produced by the previous code. The only difference is the row order, which is now sorted by product code; before, it depended on the database.

#### Fixes to the previous behavior

Two bugs in the old in-memory code are fixed. Report numbers can change in these cases:

1. **Selecting several tags counted a product once per matching tag.** The old query joined the tags, so a product with two of the selected tags had its credits and debits doubled. Now each entry is counted once.
2. **Backdated inventory corrections (CSV) could be undercounted.** The old code removed duplicate transactions with `unique()`. Because `Transaction` is `Comparable` (by transaction date, then date created), two different backdated transactions with the same dates were treated as one. Now each transaction is counted.

#### Not changed

A transaction exactly at the start of the period (midnight) is excluded from both the opening balance and the period totals, as before. On the data we checked, that affects 21 of about 700k credit/debit entries since 2025. It's left as-is and can be fixed separately if needed.

#### Results

Measured locally (1.8 GB heap, copy of production data, MariaDB):

| | Before | After |
|---|---|---|
| Submit, large facility, 8 months | 16–20s | ~12s |
| CSV, large facility, 8 months | 13–20s | ~12s |
| Concurrent requests | 10–12 caused ~90s of continuous full GCs (47), old gen ~100% | 5 at once: no full GCs, finished in ~25s |
| Live heap after the burst | – | back to the normal working set (no retained data) |

#### Tests

`ReportServiceTransactionReportSpec` (9 tests):

- credits and debits per product, including negative credits
- only the period and the facility
- products without movements are excluded
- each filter
- the CSV's per-type, adjustment and backdated columns
- the two fixes above
- a comparison against a copy of the previous implementation for 300 random transactions, with and without each filter, for the summary and the CSV

The phase 1 spec still passes. Both specs pass on MySQL 8.0.36 and MariaDB 10.3.39.

#### How to test

1. Run the report (Submit and Download Data) for a large facility over several months. Compare with the phase 1 branch or `release/0.9.9`: the values should match, apart from the row order and the two fixes above.
2. Filter by one tag, then by two tags that the same products have. The totals shouldn't double.
3. Open the details dialog for a few rows. It's unchanged and should match the summary.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RqDhKQyrN4ZX1iZUg4RvAm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `40e80a1522a2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.