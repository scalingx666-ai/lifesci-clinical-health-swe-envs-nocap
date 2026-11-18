# Issue

**Title:** ENG-1159 Fix encounter page issues in care.3.1/base

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/147/changes/care_fe/147
<!-- entire-trail-link-end -->

## Proposed Changes
Fix : [ENG-1159]
Encounter status colours differ from the shared status colour map in the EncounterHeaderDetails
<img width="1569" height="483" alt="image" src="https://github.com/user-attachments/assets/4b5b43f3-2602-4cd5-a6df-5a7fffc659b3" />


In service request list the status and priority badges stack instead of sitting on one line
<img width="1369" height="340" alt="image" src="https://github.com/user-attachments/assets/ee3adc2d-4e3b-4533-bf97-a042763f7f1b" />


Patient hover card: the buttons sit too close to the details and have too much padding
<img width="588" height="532" alt="image" src="https://github.com/user-attachments/assets/951d28ee-576b-48b9-b024-35511578eb5e" />

Fix the active overview tab and top ring merge issue
<img width="384" height="401" alt="image" src="https://github.com/user-attachments/assets/0f3e597b-2028-4f0d-bda2-ef239ca046ca" />



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


[ENG-1159]: https://openhealthcarenetwork.atlassian.net/browse/ENG-1159?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a99d1cc6ac70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.