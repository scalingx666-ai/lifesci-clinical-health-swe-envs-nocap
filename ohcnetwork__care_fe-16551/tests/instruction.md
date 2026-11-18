# Issue

**Title:** [ENG-738] fix: update encounter end date handling in EncounterQuestion component

## Description

## Proposed Changes
This PR fixes an issue with manually updating a encounter after it has been restarted.

Currently, if an encounter end date (discharge date) already exists, it is overwritten with the current date and time. Instead, the existing discharge date should be preserved. If any changes are required, the user can review and update the date manually.

This issue only occurs when the encounter is updated manually through the **update encounter.** It does not affect the **Mark as Complete** flow, as that path handles the encounter correctly. Therefore, this is an edge case specific to manual updates is fixed here.

<img width="1671" height="966" alt="image" src="https://github.com/user-attachments/assets/995fdfb7-7eb8-4314-b742-07611bfd9dc0" />



Fixes ENG-738

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

* **Bug Fixes**
  * Improved questionnaire loading and error handling with clearer loading states.
  * Encounter responses now reliably retain existing server or locally entered values.
  * Terminal encounters keep their end date synchronized, with the current date and time used when none is available.
  * Non-terminal encounters clear outdated end dates, while outpatient and discharge details are handled more consistently.
* **Style**
  * Improved text wrapping for hospitalization section headings.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `038a33ff9de1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.