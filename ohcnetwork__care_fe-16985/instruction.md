# Issue

**Title:** [ENG-19] Updating the specimen definition slug throws 404

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/116/changes/care_fe/116
<!-- entire-trail-link-end -->

## Proposed Changes

[ENG-19]

On the specimen definition edit page, after updating the slug, the success page redirects to the view page, but the URL still contains the old slug, causing an error when loading the page. Fixed this by updating the URL with the latest slug.

https://github.com/user-attachments/assets/decf0e0b-7bc7-4818-8498-5d0671079ce0

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

[ENG-19]: https://openhealthcarenetwork.atlassian.net/browse/ENG-19?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Improvements**
  * After creating a specimen definition, users are taken to the definitions list. After updating one, they’re taken to that definition’s page.
  * When a custom completion action is provided, it runs instead of the default navigation.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8c45c609cc38`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.