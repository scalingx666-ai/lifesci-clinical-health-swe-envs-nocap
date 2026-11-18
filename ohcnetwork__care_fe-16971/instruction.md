# Issue

**Title:** [ENG-1097] fix: change the limit of pinned links to be per facility

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/103/changes/care_fe/103
<!-- entire-trail-link-end -->

Updates the logic for managing pinned dashboard links so that the maximum number of pinned links is enforced per facility, rather than globally. It introduces a new test to verify this behavior and updates the UI and user feedback accordingly.

[ENG-1097]

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes

[ENG-1097]: https://openhealthcarenetwork.atlassian.net/browse/ENG-1097?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Pinned links are managed separately for each facility, with a limit of 10 links per facility. The Overview displays links for the selected facility, as well as links not assigned to a facility.
  * Resetting pinned links for one facility no longer removes links saved for other facilities. Already-pinned links remain eligible when checking whether another link can be added.
  * The pin-limit message now clarifies that the maximum applies to the facility.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57205b897804`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.