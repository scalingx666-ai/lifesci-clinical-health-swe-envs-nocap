# Issue

**Title:** [ENG-1174] Fix dispenses not listed when incomplete filter is applied in prescription preview table

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/155/changes/care_fe/155
<!-- entire-trail-link-end -->

Entire-Checkpoint: 70b13d6a2599

## Proposed Changes

ENG-1174

- Fix dispenses not listed when incomplete filter is applied in prescription preview table

<img width="1705" height="674" alt="image" src="https://github.com/user-attachments/assets/c8f4eae5-3620-481e-adc5-a7bfc3cf72f1" />

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [x] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Prescriptions with no dispense status now appear when filtering for incomplete prescriptions.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `81e7515fdf4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.