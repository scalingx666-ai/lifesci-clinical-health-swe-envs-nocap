# Issue

**Title:** [ENG-790] feat: enhance prescription print

## Description

## Proposed Changes

Fixes ENG-790

<img width="1281" height="1032" alt="image" src="https://github.com/user-attachments/assets/d7ea0c9d-5326-4f59-aaaa-dd835a154bd9" />


Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **New Features**
  - Enhanced prescription printouts with a redesigned patient header, context-based encounter/location visibility, smaller QR sizing, an “[x of y]” indicator, and improved medication instruction grouping.
  - Added an optional custom footer to print previews.
  - Expanded print table rendering with customizable table/header/cell styling and merged-row support.

- **Improvements**
  - Updated dosage rounding/display consistency and tightened dosage highlight spacing.
  - Preserved line breaks in dispense order table cells.

- **Localization**
  - Added new English UI strings for dosage/instruction labels and counters.

- **Tests**
  - Updated Playwright assertions to match the updated UI formatting and row matching logic.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d120d876624`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.