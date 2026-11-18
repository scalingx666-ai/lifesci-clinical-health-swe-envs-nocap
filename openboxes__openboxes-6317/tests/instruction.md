# Issue

**Title:** OBPIH-7878 Exclude internal transfers from the transaction report

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** [OBPIH-7878](https://pihemr.atlassian.net/browse/OBPIH-7878), #6201

**Description:**

Leaves internal transfers out of the transaction report, and lists products with stock even when they had no credits or debits in the period. On top of #6309 (merged).

**Internal transfers (OBPIH-7878)**
- A putaway, stock transfer or bin replenishment is recorded by `InventoryService.transferStock` as a Transfer Out and a Transfer In at the same facility, linked by a `local_transfer`. It moves stock between bins without changing the facility's quantity on hand, but the report counted both sides as a credit and a debit.
- The credits, debits and CSV Transfer In/Out columns now leave out a transfer whose linked transfer is at the same facility (two `NOT EXISTS` checks on the indexed `local_transfer` columns). A local transfer between two facilities (e.g. from a request) is still counted. Each pair cancels out, so Differences doesn't change.
- An **Include internal transfers** checkbox (off by default) counts them again, which gives the same numbers as before.
- In the details dialog, internal transfers are dimmed with a tooltip and don't change the balance, but they still update each bin's quantity, so the unrecorded change rows at a later count stay correct. They're hidden unless **Include internal transfers** is checked in the dialog.

**Products listed**
- The report only listed products with a credit or debit in the period, so a quiet period returned nothing, and a product whose only activity was a count didn't appear (since #5358). It now lists every product that matches the filters and had stock at the start or end of the period, or a credit or debit during it.
- An **Include products with no activity** checkbox (off by default) controls whether products whose credits, debits and differences are all 0 are listed. With it off, the report lists the products with activity, as before, plus products that were only counted.
- The CSV download uses both checkboxes, so it matches the table.

**Performance**
- The opening and closing balances are now calculated for every product at the facility instead of only the ones with credits or debits. Each takes about 5s at the Distribution Center (reading ~515k transaction entries), so they now run at the same time on two connections (`GparsService.withPool` + `withNewSession`; only ids go to the other threads and they return plain totals). The internal transfer check adds no measurable time to the totals query (~0.9s either way).

Distribution Center, local copy of PIH data (MariaDB 10.6):

| | Sep 2026 | 1 Jan – 31 Oct 2026 |
|---|---|---|
| Report, #6309 | 11.0s / 11.3s | 12.3s / 12.1s |
| Report, this PR | 9.1s / 8.7s | 9.0s / 8.9s |
| CSV, #6309 | 11.2s | 12.5s |
| CSV, this PR | 9.4s | – |

Effect on the numbers, Sep 2026:

| | Products | Credits |
|---|---|---|
| #6309 | 673 | 10,993,288 |
| This PR (defaults) | 651 | 6,373,754 |
| Include products with no activity | 1,873 | 6,373,754 |
| Include internal transfers | 673 | 10,993,288 |

22 products had only internal transfers in September. Over 1 Jan – 31 Oct, internal transfers were 86.3M of the 181.7M credits (48%).

Known edge case: 6 of the 107,434 internal pairs in this data have different dates on the two sides (2020 and 2024). A period boundary between them would show half of the pair as a difference.

**Testing**
- `ReportServiceTransactionReportSpec`: new tests for products with stock or only a count but no credits or debits (listed only with Include products with no activity), and for internal transfers (left out by default, counted with Include internal transfers, a transfer to another facility always counted, CSV Transfer In/Out columns). The comparison with the previous implementation allows the extra products, as long as they have no credits or debits. The spec calculates the balances one after the other, because other connections can't see its rolled-back test data.
- `ReportServiceTransactionReportModalDataSpec`: new test for an internal putaway between two bins followed by a count that matches each bin (no unrecorded change rows, balance unchanged).
- Checked in the browser on a copy of PIH data: both checkboxes, the CSV, and the dialog toggle (product 11085, whose only September activity was one internal pair).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RqDhKQyrN4ZX1iZUg4RvAm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e01935ebba7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.