# Issue

**Title:** #6201 Summarize the transaction report details and metadata

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** #6201

**Description:**

Follow-ups to the transaction report changes in #6309 and #6317 (merged):
- summaries in the details dialog and the Report Metadata box
- links to the previous and next period
- the report's settings in the URL
- a faster details dialog
- cleanups from the earlier reviews

**Details dialog**
- **Summary at the top**, like a bank statement: `Opening` + credits − debits ± differences = `Closing`.
  - The opening and closing balances are shaded, to set them apart from the period's activity between them.
  - Credits, debits and differences carry their sign (+ / −) instead of the report's parentheses, which would read as a double negative.
  - Clicking credits, debits or differences shows only those rows. A "Showing: … Clear" label appears in the table's search row while a filter is on.
- **Two tabs:**
  - **Transactions:** the existing table. The tab shows the number of transactions, with the breakdown (transactions, counts, internal transfers) in its tooltip.
  - **By type:** the number of transactions, credits, debits and net per transaction type. Counts, unrecorded changes and internal transfers have their own rows. The Total row's credits and debits match the summary. Clicking a type switches to Transactions, filtered to that type.
- **Include internal transfers** is now on the right of the tab bar, with the number of internal transfers. It starts checked when the report was run with it, so the summary always matches the product's row.
- The header takes two rows (summary, tab bar), so more of the table fits in the dialog.

**Report Metadata**
- **The settings the report ran with**, so that two runs can't differ with no visible reason:
  - **Filters:** category, formulary, tags, products.
  - **Included:** the two "Include …" checkboxes.
- **Counts that filter the table**, each a link with a Clear link next to it:
  - **With differences:** the count plus the net quantity.
  - **Stockouts:** stock at the start of the period, none at the end.
  - **Negative closing.**
- The box describes the report that was run, not the current state of the form.

**Previous / Next period**
- Links above the Period field move to the period before or after the selected one, keeping its length. They don't re-run the report.
- **How the length is kept:**
  - A period chosen with a shortcut keeps that shortcut's length, so "This quarter" steps back by whole quarters and "Last 7 days" by 7 days.
  - Otherwise, whole months step by months and anything else by its number of days.
- **Limits:** the end date is capped at today, and Next is disabled when the next period would start after today. Each link's tooltip shows the period it moves to.

**Settings in the URL**
- Running the report puts its settings in the page's URL (`history.replaceState`, so no extra history entries), with `run=true`. Reloading the page or opening a shared link runs the same report.
- `ReportController.showTransactionReport` fills the facility, dates and products from the URL. Category, formularies, tags and the checkboxes were already filled from the request.
- "Include all products in all subcategories" stays checked by default, but a report link leaves it unchecked if it was unchecked.
- The CSV download builds its request from the same function as the URL.

**Faster details dialog**
- **Before:** the dialog took about 8s for a product with a long history (Gauze 10569 or Paracetamol 10521 at the Distribution Center, local copy of PIH data on MariaDB 10.6).
- **Cause:** both balances use `getQuantityOnHandAtDate`, which took about 4s each, as long for one product as for the whole facility. With a product filter, MariaDB still started from `transaction_type` and read every transaction of each type at every facility.
- **Fix:** for 100 products or fewer, the query now starts from the products' inventory items, then their entries and transactions (`STRAIGHT_JOIN`). Larger lists, and all products, keep the current plan.
- **Effect:** the dialog now takes about 0.5s, with the same balances. The report's Products filter benefits too.

Query time (MariaDB 10.6):

| Products | Current plan | Starting from the products |
|---|---|---|
| 1 | 3.8s | 0.18s |
| 50 | 3.8s | 0.02s |
| 500 | 3.8s | 0.26s |
| 1,000 | – | 3.9s |
| 3,000 | 5.0s | 33.4s |

Results were identical for each pair.

**Fix**
- The details dialog read the facility and dates from the form when a row was clicked. Changing the period without re-running the report opened the dialog for a different period than the table showed. It now uses the settings of the report that was run.

**Cleanups** (from the reviews of #6263, #6264 and #6265)
- `@Transactional(readOnly = true)` on the two report actions in `JsonController`. The service's own annotation had no effect, because the controller's class-level `@Transactional` had already started a read-write transaction.
- `SelectTagLib.selectTags` / `selectCatalogs` use `select new map(...)` instead of collecting arrays.
- `products*.id?.unique()` in `getQuantityOnHandAtDate`.
- Removed the dead `"bSearch": false` option (DataTables 1.x uses `bFilter`) from the report and dialog tables.
- **`ProductAvailabilityServiceQuantityOnHandAtDateSpec`:**
  - `setup()` instead of a helper called from each test
  - a `transactionEntry(item:, bin:, quantity:)` helper instead of `[item, bin, quantity]` lists
  - `assert` before every assertion
  - `where:` blocks running the count tests with both product inventory and inventory baseline
  - the tie test uses one of each
- `assert` before every assertion in `ReportServiceTransactionReportModalDataSpec`.

**Testing**
- `ProductAvailabilityServiceQuantityOnHandAtDateSpec` (14), `ReportServiceTransactionReportModalDataSpec` (8) and `ReportServiceTransactionReportSpec` (10) pass. The QoH spec covers both join orders: product lists, and `null` or `[]` for every product.

Checked in the browser on a local copy of PIH data (Distribution Center, Sep 2026):

| Area | What was checked |
|---|---|
| Report Metadata | 651 products, 1 with differences (−6,800), 19 stockouts. Each count filters the table, and Clear restores all rows. |
| Details dialog | The summary reconciles with the report row (18,200 +200 −200 −6,800 = 11,400). The filters, the internal transfers toggle and By type rows work. |
| Previous / Next | Stepping from last month, This quarter, Last 7 days, This year and Yesterday. Next is disabled at today. |
| URL | A run with a formulary and Include internal transfers writes the URL, and reloading it re-runs the same report (673 products with internal transfers). |
| Tag and formulary lists | They match the database (163 tags, 35 formularies). |

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RqDhKQyrN4ZX1iZUg4RvAm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0aae5ba93a33`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.