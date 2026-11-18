# Issue

**Title:** [ENG-964] Removed encounter class update option and encounter_class_history usage

## Description

Entire-Checkpoint: 33025b100e52

## Proposed Changes

Fixes: [ENG-964]
- Removed the usage of encounter class history and the update encounter class feature fromt the Update encounter page
- Hide the mark as discharge button for non-hospitalized classes
- Changed type according to the BE change
- Updated Playwright test too

https://github.com/user-attachments/assets/84418571-69e9-44df-a4be-266b405938e3


Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

## UI Updates

* **UI Updates**
  * Encounter class badges now appear as non-interactive labels with an icon and translated name.
  * Removed the encounter class-history popover, dropdown indicator, and history listing.
  * Encounter class selection is no longer available in questionnaire encounter fields.
  * Hospitalization details now display based on the encounter’s recorded class.

* **Bug Fixes**
  * Encounter class remains unchanged when updating an encounter; status and priority updates continue to work as expected.

* **Cleanup**
  * Removed unused class-history translations and related data representations.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

[ENG-964]: https://openhealthcarenetwork.atlassian.net/browse/ENG-964?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6aa9ca0baccb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.