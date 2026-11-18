# Issue

**Title:** [ENG-1105] Fix inline delivery entry and receipt cancellation

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/111
<!-- entire-trail-link-end -->

## Jira

Related to [ENG-1105](https://openhealthcarenetwork.atlassian.net/browse/ENG-1105).

## Proposed Changes

Saving several items in the same delivery order concurrently can fail on backend row locks. Keep the existing inline controls and allow one pending addition or edit at a time, with save/discard before switching items. Request-order selection also loads one item at a time.

Cancellation now stays available after partial or full receipt, using the backend stock reversal and availability checks. Refresh delivery items, history, linked request quantities and stock caches after status changes so cancelled rows no longer remain In Progress until reload. Prevent overlapping receipt and order-status updates and explain stock reversal in the confirmation.

Add regression coverage for single-item request loading and cancellation of pending, partially received and completed orders, including persisted stock reversal. Update the internal delivery tests for single-item selection.

## Validation

- Production build and TypeScript checks passed.
- Changed-file ESLint, Prettier and `git diff --check` passed; ESLint retains the existing React Hook Form compiler warning.
- Playwright against the local backend: **11 passed** (9 external delivery cases and 2 internal dispatch/receive cases).
- Cancellation regressions fail before the repair and pass afterward; receipt cases verify stock returns from 10/25 units to zero.
- Independent review found no remaining actionable issues.

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes.

[ENG-1105]: https://openhealthcarenetwork.atlassian.net/browse/ENG-1105?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added clearer confirmation messages when abandoning a delivery order or marking it as entered in error, including the effects on active items and stock.
  * Supply requests can now be selected and added one at a time when creating a delivery.
* **Updates**
  * Delivery orders can be updated one item at a time, with pending changes and failed items handled individually.
  * Eligible external delivery orders now offer status actions independently of whether deliveries have been completed.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `472d44eb0a0b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.