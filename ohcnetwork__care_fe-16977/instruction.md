# Issue

**Title:** [ENG-1105] feat: support editing draft delivery items

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/109
<!-- entire-trail-link-end -->

## Jira

- Core: [CARE-401](https://openhealthcarenetwork.atlassian.net/browse/CARE-401)
- Engineering: [ENG-1105](https://openhealthcarenetwork.atlassian.net/browse/ENG-1105)
- Feedback source: [CIMPL-300](https://openhealthcarenetwork.atlassian.net/browse/CIMPL-300)

## Proposed Changes

Draft external delivery items require cancellation and manual re-entry to correct. Add an Edit / Continue editing flow that prefills a pending row and saves each replacement through the existing atomic cancel-and-create batch API. Originals stay active until saving, and failed drafts remain available to retry.

- Keep product knowledge fixed on saved lines. Require explicit pack quantities for new/imported items and preserve quantities through batch selection.
- Hide abandoned/error entries behind a history toggle, pin medicine names, and keep row actions in the three-dot menu. At 320px, keep medicine names visible while leaving room for editable fields.
- Preserve entered purchase totals through metadata edits and failures. Use configured accounting precision for purchase calculations and comparisons; allow existing cost corrections without inventing missing batch/expiry metadata.
- Give each newly created priced Product an independent pricing definition, preserving extensions, configuration, components, and tags. Reuse cached definitions only while unattached to a Product, including after quantity changes and preparation failures.
- Use configured accounting precision for monetary display, entry validation, and input steps (default 2 decimals / 0.01). Preserve raw stored pricing amounts until explicitly edited, so focusing a rounded field or changing unrelated metadata does not rewrite saved prices.
- Reuse the existing default date utilities for expiry display and entry. Retain the exact stored timestamp when expiry is unchanged, and serialize changed dates at local midnight so the selected date survives a save and reload.
- Refresh delivery-order summaries after item/status changes, including partial saves, so server-provided extension totals update.

No backend files or endpoints changed. Concurrent replacements from separate clients remain subject to the existing backend status-transition behavior; this frontend change does not add server-side conflict detection.

## Validation

- `npx tsc --noEmit` passed.
- Targeted ESLint, Prettier, and `git diff --check` passed. ESLint retains the existing React Hook Form `watch()` compiler warning.
- Playwright: `externalDeliveryEdit.spec.ts` passed against the local backend (**5 passed, 31.7s**, fully parallel with 4 workers). Fixtures use independent Product Knowledge and pricing definitions.
- Coverage includes explicit quantity entry and clear/refill, locked product selection, atomic rollback/retry, quantity changes after preparation, Product creation failure/retry, pricing isolation and metadata preservation, legacy cost corrections, and summary refresh after full/partial saves.
- Reproduced review defects before fixing them. Verified configured price display/steps, focus/blur without rounding stored prices, third-decimal rejection at the default precision, and explicit price persistence. Verified expiry round trips in an America/Los_Angeles browser and readable quantity/expiry fields with sticky medicine names at 320px.

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Edit in-progress delivery items, review pending changes, and save or discard edits.
  * Continue editing deliveries already being edited, with clear indicators for edits in progress.
  * View active deliveries by default and toggle cancelled delivery history when available.
  * Replace saved delivery items while retaining the original until replacement changes are saved.
  * See a notice to save or discard delivery changes before updating an order.
  * Assign a type to new items.
* **Bug Fixes**
  * Require pack quantity and pack size to be whole numbers greater than zero.
  * Preserve unsaved changes after save failures and refresh delivery summaries after successful saves.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

[CARE-401]: https://openhealthcarenetwork.atlassian.net/browse/CARE-401?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ
[ENG-1105]: https://openhealthcarenetwork.atlassian.net/browse/ENG-1105?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ
[CIMPL-300]: https://openhealthcarenetwork.atlassian.net/browse/CIMPL-300?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60f49fb358cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.