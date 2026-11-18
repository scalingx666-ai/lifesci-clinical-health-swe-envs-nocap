# Issue

**Title:** [Lab Order UI] surface preliminary and partial lab results end to end

## Description

- The Completed tab only queried `DiagnosticReport?status=final,corrected,amended`, so an order whose only result so far is preliminary or partial (e.g. an interim multi-day culture value) had nowhere to show up - Open lists the order itself with no indication a result exists, and Completed excluded it outright
- Widen the default status filter to include `preliminary,partial` (deliberately excluding `registered`, which has no result content yet)
- The Report tab itself was also gated on `order.status === 'completed'` rather than on whether a report existed - once a preliminary/partial report is listed under Completed, clicking it had nowhere to render its content either, since the one tab that could show it doesn't exist while the order is still in progress
- Make the Report tab's presence depend on whether a report resolved, independent of order status, and default to it whenever the caller explicitly selected a report
- Add test coverage for each tab's default status filter and for a preliminary result attached to a still-in-progress order

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f970ecb8478e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.