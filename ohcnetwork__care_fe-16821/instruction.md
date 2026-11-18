# Issue

**Title:** Add round whole for account balance

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/10
<!-- entire-trail-link-end -->

Entire-Checkpoint: c6b215177c63
This pull request updates the way monetary values are displayed and styled in the account billing UI. The main change is that all account balances and gross totals are now rounded to whole numbers before being shown to users and before determining their styling (such as color and text). This ensures consistency and avoids confusion from displaying fractional values.

**Monetary Value Rounding and Display:**

* All uses of `account.total_balance` and `account.total_gross` in both `AccountList.tsx` and `AccountShow.tsx` are now passed through the `roundWhole` function before being displayed or used for styling logic. This affects the `MonetaryDisplay` components and conditional styling for positive/negative balances. [[1]](diffhunk://#diff-910f5cce6c80285ee1c2fd728a3c330a621390a497ee68847b906ab32c540e78L290-R297) [[2]](diffhunk://#diff-39f6b67ba4d7e4159f564c2cfcf8e7b855b853310023258fc4b4bdd11dafdfb5L575-R587) [[3]](diffhunk://#diff-39f6b67ba4d7e4159f564c2cfcf8e7b855b853310023258fc4b4bdd11dafdfb5L612-R615) [[4]](diffhunk://#diff-39f6b67ba4d7e4159f564c2cfcf8e7b855b853310023258fc4b4bdd11dafdfb5L778-R781)

**Utility Imports:**

* The `roundWhole` function is imported from `@/Utils/decimal` in both files to support the new rounding logic. [[1]](diffhunk://#diff-910f5cce6c80285ee1c2fd728a3c330a621390a497ee68847b906ab32c540e78L58-R58) [[2]](diffhunk://#diff-39f6b67ba4d7e4159f564c2cfcf8e7b855b853310023258fc4b4bdd11dafdfb5L60-R60)

**Code Consistency and Refactoring:**

* Local variables (`roundedBalance`, `roundedBilledGross`) are introduced in `AccountShow.tsx` for clarity and to avoid redundant rounding.

These changes improve the clarity and consistency of financial data shown to users, reducing the risk of misinterpretation due to fractional amounts.

## Proposed Changes

Fixes #issue_number
- Change 1
- Change 2
- Additional context if needed

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Account balances and billed amounts are now rounded to whole numbers before being displayed across account lists, account details, and payment reconciliation.
  * Amount colors and closed-account balance notices now consistently reflect the rounded values.
  * Payment reconciliation now presents non-invoice balance-due amounts using the same whole-number formatting when a balance is available.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c22b5c208a59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.