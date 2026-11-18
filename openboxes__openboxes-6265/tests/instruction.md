# Issue

**Title:** Show progress and prevent repeat runs on the transaction report page

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** #6201

**Stacked on #6263 (phase 1). Please review that PR first.** This PR's base is the phase 1 branch, because the page builds on its Net Change column. The diff only shows this PR's changes.

**Description:**

Part of #6201. Part of the problem was the page itself: nothing showed that a report was running, so users clicked Submit or Download again. Each click started another report on the server, and a burst of these ran it out of memory. This PR makes the page show progress and prevents running the report again until the current run finishes. It also cleans up the table and speeds up the tag and catalog dropdowns.

#### One report at a time

- While a report is running, the page is covered by an overlay that shows the elapsed time and a hint not to refresh. Submit and Download Data are disabled.
- **Download Data** now downloads in the background instead of navigating to the URL. The page then knows when the download is done, can show errors, and a second click can't silently cancel the first download.
- **Errors:** a timeout, a server error (with its message), or an expired session (the login page instead of the CSV) each show a specific message.
- **Timeout:** the page waits up to `openboxes.report.transactionReport.timeout` (default 5 minutes) instead of the general AJAX timeout (2 minutes), which large reports could exceed. Download Data had no timeout.

#### Table

- Number columns are right-aligned with tabular digits, so the values line up. Zeros are dimmed.
- **Totals row:** the footer shows totals of the rows that match the search, across all pages.
- Long product and category names are limited to two lines; the full name is in the tooltip.
- **Columns stay lined up when the page width changes.** The table scrolls, so DataTables puts the header and footer in their own tables, sized when the table is drawn. When the window was resized, the rows reflowed but the header and footer kept their old widths. The columns are now resized when the window size changes.
- Row striping and hover highlighting (rows open the product's transactions when clicked).

#### Tag and catalog dropdowns (`SelectTagLib`)

The dropdowns showed each tag's or catalog's product count by loading every product of every tag (and every item of every catalog) into the Hibernate session. Now the counts come from a single query. The same dropdowns are used on the product list, inventory and consumption filters, and the forecast and request detail reports, so those pages load faster too.

#### How to test

1. Run the report for a large facility over several months. The overlay should appear with a running timer, and the buttons should be disabled until the table loads.
2. Click Download Data. The overlay should appear, then the CSV should download. Clicking again while it runs should do nothing.
3. Log out in another tab, then click Download Data. You should get the session expired message.
4. Check that the header, body and footer columns line up, including after scrolling and after making the window narrower and wider, and that the totals row changes when you search.
5. Check that the tag and catalog dropdowns show the same product counts as before here and on the product list.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RqDhKQyrN4ZX1iZUg4RvAm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `40e80a1522a2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.