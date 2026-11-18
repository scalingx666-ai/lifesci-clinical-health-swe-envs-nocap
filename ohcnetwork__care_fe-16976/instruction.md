# Issue

**Title:** [ENG-1104] fix: link delivery items to product details

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/108
<!-- entire-trail-link-end -->

## Proposed Changes

Fixes [ENG-1104](https://openhealthcarenetwork.atlassian.net/browse/ENG-1104)

Core story: [CARE-399](https://openhealthcarenetwork.atlassian.net/browse/CARE-399)

Delivery order item names previously opened delivery history, leaving no direct path to the created product. They now use dark, underlined links to the exact product batch, with a muted history button preserving access to the filtered delivery history drawer. The item column has room to keep short product names on one line.

## Validation

- `npx tsc --noEmit`
- ESLint and Prettier checks on both changed files
- Playwright browser verification: product navigation opens the matching lot; history opens the filtered drawer; desktop and mobile viewport layouts checked

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files (reuses the existing translation).
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added a dedicated history button with a tooltip to open a delivery’s history, keeping product names separate from history actions.
  * Product names in existing deliveries now link to their product pages, wrap more cleanly, and use clearer underlined styling.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

[ENG-1104]: https://openhealthcarenetwork.atlassian.net/browse/ENG-1104?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ
[CARE-399]: https://openhealthcarenetwork.atlassian.net/browse/CARE-399?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b2ac6fcff7e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.