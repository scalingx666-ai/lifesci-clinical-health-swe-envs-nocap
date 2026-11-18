# Issue

**Title:** Improve the transaction report page and details dialog

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** #6201

**Description:**

Improvements to the transaction report page and its details dialog, on top of #6265.

**Report table**
- Replaces the Net Change column with **Differences**: `closing − opening − credits + debits`. Credits and debits only include credit and debit transactions, so this is the change in quantity on hand from counts (product inventory and baseline transactions) that didn't match the balance before them, i.e. the part of the change that credits and debits don't account for. It's 0 for most products. Net Change (`closing − opening`) only repeated what the other columns already show, and hid count differences inside it.
- The CSV export gets the same Differences column, before Closing.
- Adds a tooltip to every column header (dotted underline, help cursor).
- Removes the totals footer. Summing quantities across hundreds of different products doesn't produce a meaningful number.
- Column widths: product code and name side by side, a wider category, and the quantity columns narrow and on the right.
- The empty table says what to do ("Choose a facility and period, then click Run Report.") before a report has been run, and that no products had credits or debits when a report has no rows. The empty row isn't clickable or highlighted.
- The table is titled **Report Details**.

**Parameters**
- Facility, then the period, then an optional "Filter products" section (category, formulary, tags, products).
- The start and end dates are replaced by one **Period** field with a date range picker (the same jquery-date-range-picker 0.16.1 as the request list, with moment.js 2.29.4): two months side by side, no days after today, and shortcuts for days, months, quarters and years (e.g. last 7 days, last month, last quarter, last year). Dates can also be typed (`01/Jan/2026 - 31/Jan/2026`). Both dates are included, and the period defaults to last month.
- Run and Download CSV side by side, Download CSV has a tooltip, and Enter in a field runs the report.
- Replaces the Metadata box, which counted rows in the transaction fact table (no longer used by this report) and showed the refresh job's fire times, with a **Report Metadata** box: facility, period, number of products, when the report was generated and how long it took.
- The progress overlay covers the whole page.

**Details dialog**
- Date and time in one column (easier to scan down: the time is dimmed, a repeated date is dimmed, and a line separates days), plus the transaction (linked to the transaction page), the **reference** (the request, shipment, order or putaway it came from, linked to its page, loaded in one query), lot number and bin location.
- Opening and closing balances are shown as labeled rows.
- Credits are shown as `+n` and debits as `(n)`. Count quantities are dimmed, with a tooltip explaining that a count sets the balance instead of adding to it.
- **Unrecorded change** rows before each count, one per lot and bin, for the difference between the counted quantity and the balance before the count (including lots and bins the count left out, which it sets to 0). They add up to the Differences column. If the rows still don't add up to the closing balance, an **Unexplained difference** row shows the rest.
- When a count and a credit or debit have exactly the same dates, the count comes first, like the quantity on hand query (#6263).
- Fixes the loading spinner showing on top of "No records found".
- Wider dialog (1000px).

**Follow-ups (not in this PR)**
- The report only lists products that had a credit or debit in the period, so a quiet period returns nothing, and a product whose only activity was a count doesn't appear. This has been the behavior since #5358. It will be fixed in the next PR, along with leaving out internal transfers (OBPIH-7878) and a "Hide products with no activity" option.
- A summary in the Report Metadata box (products with differences, stockouts, negative closing balances), with links that filter the table.

**Testing**
- `ReportServiceTransactionReportModalDataSpec` (from #6308) passes, with new tests for unrecorded change rows (per lot and bin, a lot left out of a count, a count that matches, rows adding up to Differences) and for a count and a credit with the same dates.
- `ReportServiceTransactionReportSpec` (from #6264) updated for the rename (Net Change → Differences) and the CSV Differences column, and passes.
- Checked on a copy of PIH data (Distribution Center, 1 Jan – 31 Oct 2026): for all 31 products with Differences, the unrecorded change rows add up to Differences and the dialog ends at the closing balance.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RqDhKQyrN4ZX1iZUg4RvAm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a5c44ca93f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.