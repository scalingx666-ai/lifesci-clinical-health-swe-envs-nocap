# Issue

**Title:** [ENG-1133] feat: enhance item selection in AddSupplyDeliveryForm with checkbox

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/123/changes/care_fe/123
<!-- entire-trail-link-end -->

## Proposed Changes

Fixes #ENG-1133

<img width="754" height="427" alt="image" src="https://github.com/user-attachments/assets/12a40c00-c195-4a70-9b4c-0ffee43dd552" />

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Delivery submissions can include multiple items, with request orders selectable individually or all at once.
  * Selected requests are added as rows, with inward-stock pack quantities defaulting to 1.
  * A warning appears and confirmation is disabled when selections would exceed the delivery limit.
* **Improvements**
  * Before saving, replacement deliveries are checked to ensure they are still in progress.
  * Rows are saved sequentially. Successful saves trigger a success notification; if some rows fail, successful rows are removed and failed rows remain for correction. The form resets when all rows save successfully.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `872ed91f7c03`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.