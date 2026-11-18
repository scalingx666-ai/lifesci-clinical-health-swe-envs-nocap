# Issue

**Title:** [ENG-1076]: fix: update button accessibility for pinning pages

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/88
<!-- entire-trail-link-end -->

Update the accessibility of the pin/unpin button in the `PinPageDialog` component. The button is now hidden visually but remains accessible to screen readers, and it includes an appropriate ARIA label for better accessibility.

[ENG-1076]
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

[ENG-1076]: https://openhealthcarenetwork.atlassian.net/browse/ENG-1076?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Accessibility**
  * The pin-page control is now available to assistive technology with a label that reflects whether the page is pinned, while remaining out of keyboard tab navigation.
* **New Features**
  * Added English labels for the pin and unpin page shortcuts.
* **Tests**
  * Added coverage verifying that the Shift+B shortcut pins a page, provides a navigable link, and unpins the page.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f30bb8647215`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.