# Issue

**Title:** [ENG-922] Adds expiration date filter for inventory items list view

## Description

ENG-922

## Proposed Changes

- Adds expiration date filter for inventory items list view
- Switch the filter state management to use `useMultiFilter` for inventory items list view
- Adds sort by expiration date

<img width="1760" height="1214" alt="image" src="https://github.com/user-attachments/assets/a81d0036-780a-42df-a1c6-204c7430995a" />


Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [x] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **New Features**
  - Added inventory filters for status and product expiration dates, including “Expired” and “Expiring Soon” options.
  - Added sorting by net content and earliest/latest expiration date.
  - Added localized labels for expiration and sorting options.
  - Added color-coded inventory status badges and expiration warnings.
- **Improvements**
  - Enhanced date-range filtering with open-ended ranges and consistent comparisons.
  - Updated the inventory toolbar for filtering and sorting controls.
  - Improved handling of invalid expiration dates and filter values.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `07a087e44662`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.