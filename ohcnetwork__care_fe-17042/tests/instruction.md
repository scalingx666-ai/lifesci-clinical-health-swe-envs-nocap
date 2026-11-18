# Issue

**Title:** ENG-1189 Fix page jump when opening autocomplete on desktop in Patient registration page

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/162/changes/care_fe/162
<!-- entire-trail-link-end -->

## Proposed Changes

Fixes [ENG-1189]
Remove the extra input autofocus on desktop and let Base UI handle focusing the search input. This prevents the page from jumping when the dropdown opens while keeping the existing mobile behavior

https://github.com/user-attachments/assets/b15c294b-054d-4968-a594-a0b7475438f8

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

[ENG-1189]: https://openhealthcarenetwork.atlassian.net/browse/ENG-1189?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f0a60985324`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.