# Issue

**Title:** [ENG-746] Hide "completed" from encounter status

## Description

## Proposed Changes
Fixes ENG-746

**Reason for doing this** 


_The "Completed" option is still present in the Update Encounter section. It should either be removed from the list, or validation must be added to ensure that a discharge disposition is mandatory before submission. Currently, the system allows submission without adding a discharge disposition when "Completed" is selected, which is incorrect._

_Currently this is impacting our TeleICU dashboards numbers. In the attached dashboard’s screenshot, 928 patients are in not defined status due of this._


Now the "Mark as complete" should be used to complete an encounter.
If ip encounter: "discharge" -> "complete" 

<img width="1133" height="469" alt="image" src="https://github.com/user-attachments/assets/cb2bcb8b-aba0-441a-97a7-4c16cbe4fd2c" />

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
  * Updated encounter status selection rules so users can’t choose invalid options.
  * If the current encounter status is **Discharged**, **Unknown**, or **Completed**, the dropdown now shows only that current status.
  * Otherwise, the dropdown excludes **Discharged**, **Unknown**, and **Completed** to prevent incorrect transitions.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a0e326bd86a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.