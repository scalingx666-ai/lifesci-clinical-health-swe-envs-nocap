# Issue

**Title:** [ENG-847] fix: prevent autoFocus from repeatedly triggering the keyboard on iOS devices

## Description

Addresses an issue with the `autoFocus` attribute on input fields across several components, specifically to prevent undesirable autofocus behaviour on iOS devices. The main change is to conditionally set `autoFocus` based on whether the user is on an iOS device, using a new utility function `isIOSDevice`. This improves the user experience by avoiding unwanted keyboard pop-ups and focus issues on iOS.

[ENG-847]

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

## Bug Fixes

* Improved search and selection experiences on iOS by preventing automatic focus in category pickers, role selectors, medication selectors, questionnaire search, autocomplete fields, and device selectors.
* This prevents the on-screen keyboard from opening unexpectedly and keeps screens positioned naturally when opened.
* Automatic focus remains available on non-iOS devices.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

[ENG-847]: https://openhealthcarenetwork.atlassian.net/browse/ENG-847?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `64bb6d516022`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.