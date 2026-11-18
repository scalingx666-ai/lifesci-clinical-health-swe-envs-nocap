# Issue

**Title:** [ENG-784] Encounter Action button is clipping out

## Description

## Proposed Changes

Fixes [ENG-784]

<img width="1514" height="378" alt="image" src="https://github.com/user-attachments/assets/ec458ba7-5dea-4a03-b877-7848760474c4" />


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

[ENG-784]: https://openhealthcarenetwork.atlassian.net/browse/ENG-784?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Style**
  * Updated the layout structure around encounter quick actions for improved rendering consistency.
  * Made the quick-actions container responsive by using full width on smaller screens and automatic width on medium and larger screens.
  * Preserved the existing appearance of the patient information quick-action button (including gradient styling and typography).
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `70b29729cd65`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.