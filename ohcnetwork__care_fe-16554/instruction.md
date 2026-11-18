# Issue

**Title:** [ENG-735] Add pagination in Dispense History selector

## Description

## Proposed Changes

Fix : [ENG-735]

https://github.com/user-attachments/assets/b19a561f-1027-41a2-a9f0-51b33fd7ce36


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

[ENG-735]: https://openhealthcarenetwork.atlassian.net/browse/ENG-735?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added infinite scrolling to dispense order lists, automatically loading additional orders as users reach the end.
  * Added a loading indicator while more dispense orders are being fetched.

* **Bug Fixes**
  * Improved default selection behavior by automatically selecting the first available dispense order.
  * Prevented the list from rendering when no dispense orders are available.
  * Improved list handling as additional dispense orders are loaded.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8160376515fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.