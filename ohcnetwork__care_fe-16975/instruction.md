# Issue

**Title:** [ENG-1103] Streamline pharmacy invoice issuance and payment collection

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/107
<!-- entire-trail-link-end -->

## Proposed Changes

Fixes [ENG-1103](https://openhealthcarenetwork.atlassian.net/browse/ENG-1103)

Core story: [CARE-398](https://openhealthcarenetwork.atlassian.net/browse/CARE-398)

Pharmacy billing now creates and issues the invoice, then opens Collect Payment automatically. Bill Selected shows a preparation overlay throughout the operation and keeps selected rows mounted while prescription data refreshes.

- Use the existing draft-create and invoice-update APIs; recover the saved draft/order when issuance fails without repeating dispensing or invoice creation.
- Consume the payment-opening request once, preserving other navigation parameters.
- Automatically balance issued, non-refund invoices when confirmed payments minus credits exactly match the invoice total. Keep the receipt open and preserve a balance-only retry if that update fails.
- Prevent stale invoice refetches from overwriting the balanced state.

All changes are frontend-only.

## Validation

- TypeScript typecheck passed.
- Changed-file ESLint and Prettier checks passed; existing React Hook Form compiler warnings remain.
- Desktop Playwright checks with mocked writes covered create/issue success and failure, draft retry without duplicate creation, payment opening once, navigation parameter consumption, and settled-invoice handling.
- Eight mocked payment scenarios covered exact payment, final installment, underpayment, overpayment, credits, balance failure/retry, and a delayed invoice-refetch race.
- Billing transition checks covered slow save/create/issue requests, background refetches, duplicate-submission prevention, preserved selections after save failure, and draft recovery after issuance failure.

Browser checks used temporary scripts; no persistent test specs were added. Mobile QA and live payment-write testing were not performed.

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices (mocked writes).
- [ ] Add or update Playwright tests for related changes.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Pharmacy billing now creates and issues invoices in one flow, then opens payment collection for the issued invoice when applicable.
  * Eligible payments can automatically balance an invoice; a manual balance option remains available when needed.
  * Billing displays a progress message while invoice preparation is underway.
* **Bug Fixes**
  * Prevented repeat submissions while billing is in progress.
  * Payment records remain saved if automatic invoice balancing fails.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

[ENG-1103]: https://openhealthcarenetwork.atlassian.net/browse/ENG-1103?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ
[CARE-398]: https://openhealthcarenetwork.atlassian.net/browse/CARE-398?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b5066744940`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.