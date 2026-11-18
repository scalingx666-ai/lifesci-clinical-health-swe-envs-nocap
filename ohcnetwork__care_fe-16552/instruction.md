# Issue

**Title:** Remove unneeded defensive code in useMultiFilterState

## Description

## Proposed Changes

Addresses a CodeQL code-quality finding (`js/unneeded-defensive-code`) in `useMultiFilterState`. Inside `getInitialValues`, the query-param handling is already wrapped in `if (queryValue)`, so `queryValue` is guaranteed truthy in every branch. The final `else if (queryValue !== null && queryValue !== undefined)` therefore always evaluates to true, which CodeQL flagged as unneeded defensive code.

- Replaced the redundant `else if (queryValue !== null && queryValue !== undefined)` with a plain `else`. This is behavior-preserving: the only reachable cases at that point (number, boolean, bigint, symbol) are all truthy, so the fallthrough coercion via `String(queryValue)` is unchanged.

Verified by running the exact CodeQL query (`Expressions/UnneededDefensiveProgramming`) locally against a fresh database before and after the change: the finding drops from present to zero, with no other live occurrences of this rule in the codebase.

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

N/A - internal refactor with no behavior change; not user-facing and adds no UI text.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Improved multi-filter handling for query parameters with non-standard or empty values.
  * Ensured remaining filter values are consistently converted into a usable format.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47abd7fa045b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.