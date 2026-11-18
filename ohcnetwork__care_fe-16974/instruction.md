# Issue

**Title:** [ENG-896] feat: implement FEFO inventory fetching and auto-select for DispenseDrawer

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/106
<!-- entire-trail-link-end -->

## Proposed Changes
This old PR for FEFO "" was closed in fav of pharmacy but the dispense in encounter was missed out.

Fixes ENG-896

<img width="1326" height="572" alt="image" src="https://github.com/user-attachments/assets/6917447a-b7bd-4802-a36e-4389cef40af7" />

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

* **Bug Fixes**
  * Dispensing now prioritizes eligible inventory lots by earliest expiration date and excludes products that expire before the dispensing threshold.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b5066744940`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.