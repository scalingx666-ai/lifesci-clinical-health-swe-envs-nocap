# Issue

**Title:** [ENG-744] Highlight dosages when they aren't 1

## Description

Highlight everywhere except prints

<img width="2182" height="261" alt="image" src="https://github.com/user-attachments/assets/9207edd7-7bdf-4df1-893a-11fbe2e42be7" />



Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added a shared dosage formatting component and rolled it out across medication lists, administration views, dispense history, pharmacy workflows, and questionnaire/record screens.
  * Dosage values classified as non-unit (e.g., ranges or non-1 quantities) are now visually highlighted.
  * When dosage data is missing, a configurable fallback (such as `-`) is shown.

* **Improvements**
  * Refined pharmacy payment displays (localized reference label and improved timestamp formatting).
  * Medication dispense updates now use a consolidated batch update approach.

* **Tests**
  * Added assertions for yellow highlight presence for non-unit dosages and absence for unit dosages.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8160376515fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.