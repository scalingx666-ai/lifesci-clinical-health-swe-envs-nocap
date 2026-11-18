# Issue

**Title:** [ENG-1053] fix: shortcut for mark as completed and dispense actions in Encounter

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/46
<!-- entire-trail-link-end -->

fixes :  ENG-1053

Entire-Checkpoint: 9558aecbfbc2

## Proposed Changes
Fix the MC not working plus updated the playwright test


https://github.com/user-attachments/assets/0cc41d81-3dbd-45d6-be00-ae2e5cd8f7d3



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

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Accessibility**
  * Actions for marking an encounter complete and dispensing remain visually hidden but available to screen readers. They are excluded from keyboard tab navigation, while their actions and shortcut badges remain available.
* **Bug Fixes**
  * The encounter completion shortcut now follows the appropriate flow for each encounter type: confirmation for ambulatory encounters, and discharge questionnaire followed by confirmation for inpatient encounters.
  * The primary encounter loading indicator now reflects ongoing data fetching.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `958812e474ea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.