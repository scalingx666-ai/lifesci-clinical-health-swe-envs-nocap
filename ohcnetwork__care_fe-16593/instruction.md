# Issue

**Title:** [ENG-799] Display Note along with Medicine name in Grouped medicine administration

## Description

ENG-799
<img width="495" height="605" alt="image" src="https://github.com/user-attachments/assets/028ded11-0f69-4fc7-a4ec-7098211d0c80" />
<img width="699" height="261" alt="image" src="https://github.com/user-attachments/assets/f7f4a912-d986-45db-9bae-6867392ad794" />


## Proposed Changes

Fixes #issue_number
- Change 1
- Change 2
- Additional context if needed

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
  * Added medication notes to prescription lists and medication administration views.
  * Notes are shown conditionally, with preserved line breaks and subtle italic styling for readability.

* **Documentation**
  * Added clarification on how medication window start/end marker times are derived, including the case where date changes can affect the displayed time portion.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e67ba29be276`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.