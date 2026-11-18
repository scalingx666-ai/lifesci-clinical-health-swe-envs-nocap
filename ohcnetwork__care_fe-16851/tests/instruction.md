# Issue

**Title:** feat: add tooltips for amount due and billed gross in AccountShow component

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/36
<!-- entire-trail-link-end -->

## Proposed Changes

Added a tooltip showing the amount before roundoff

<img width="779" height="189" alt="image" src="https://github.com/user-attachments/assets/2c9ed9bb-ab0f-4699-8eb1-05aed40a9b1b" />

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added hover tooltips to the “Amount Due” and “Billed Gross” labels.
  * Tooltips display the corresponding unrounded account amounts.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `305d4ebbd141`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.