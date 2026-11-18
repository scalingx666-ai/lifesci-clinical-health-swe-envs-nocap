# Issue

**Title:** [ENG-1098] Adds support for printing multiple prescriptions in pharmacy related workflows

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/126/changes/care_fe/126
<!-- entire-trail-link-end -->

> [!NOTE]
> **JIRA Ticket: ENG-1098**

## Proposed Changes

- Adds support for printing selected prescriptions in prescription queue page.
- Adds support for printing all prescriptions in prescriptions preview page.
- Adds support for printing all prescriptions related to a dispense order in dispense order view page.
- Cleaned up component composition of prescription prints.

<img width="1916" height="1182" alt="image" src="https://github.com/user-attachments/assets/91b57a58-0a55-4516-a4f7-3b16252f6a76" />

<img width="1951" height="1182" alt="image" src="https://github.com/user-attachments/assets/9af49949-1530-443a-a9bb-5c73fb3cc249" />

<img width="1947" height="1183" alt="image" src="https://github.com/user-attachments/assets/fed78f4a-3429-4a28-a2b5-7884ae5ab7d9" />

<img width="1388" height="1175" alt="image" src="https://github.com/user-attachments/assets/f61c2f30-73d3-43c0-8c3d-bddd23bdae7d" />

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

* **New Features**
  * Added options to print an individual prescription or selected prescriptions from pharmacy workflows, including prescription previews and dispense orders.
  * Added printing for prescriptions associated with an encounter, with loading and no-prescriptions messages when applicable.
  * Print actions use labels suited to one or multiple prescriptions. In the prescription queue, preview, print, and billing actions are hidden when no prescriptions are selected.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28a733d21d09`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.