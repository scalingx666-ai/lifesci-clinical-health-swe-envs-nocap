# Issue

**Title:** [ENG-1153] Fix few issues in 3.1/base

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/144/changes/care_fe/144
<!-- entire-trail-link-end -->

## Proposed Changes
NAV-1,2,3, 6 and UI-2

NAV-1
Fixes: Search page actions lists the page's shortcuts, but choosing one does nothing
- now it trigger the related shortcuts
https://github.com/user-attachments/assets/cfc0d990-1522-460b-ab3c-3d8f51068a13

NAV-2
Fixes: Shift + ? doesn't open the page actions popup
- now the "shift + ?" will open the page actions
<img width="1498" height="755" alt="image" src="https://github.com/user-attachments/assets/de0f6965-caab-4a22-bfc9-186dfd2323e5" />

NAV-3
Fixes: The new header bar adds an unwanted scroll on several pages and header of clinical getting clipped
<img width="1498" height="755" alt="image" src="https://github.com/user-attachments/assets/c61ee033-6b81-4ff3-81b3-b0520f3a2030" />

NAV-4
Fixes: The sidebar keeps its last scroll position when you go into a section
- now the scroll will be on top always 
https://github.com/user-attachments/assets/99282a46-4c28-4eea-b719-e3dcba7cc5df



NAV-6
Fixes: Put "Search patients" in the sidebar, as in the CareUl demo
<img width="1498" height="755" alt="image" src="https://github.com/user-attachments/assets/9ae66c92-668e-4a67-8ff3-618c314b8546" />


UI-2 
Fixes: The "Create Schedule Template" sheet heading needs cleanup
<img width="1498" height="755" alt="image" src="https://github.com/user-attachments/assets/d951a062-eb3b-4136-b45c-9094438dc711" />


Fixes: the form, quick actions getting clipped 
<img width="1498" height="755" alt="image" src="https://github.com/user-attachments/assets/544931a1-01b1-4173-8754-3f797c8ec2ec" />



Fixes ENG-1169
- Here the shortcut was not working will for "Add charges. Press Enter to start searching."
<img width="1212" height="824" alt="image" src="https://github.com/user-attachments/assets/f5d0e4e1-f399-412c-a486-2b382674313c" />

- Here both "Add charges. Press Enter to start searching." and submit shortcut
<img width="1212" height="824" alt="image" src="https://github.com/user-attachments/assets/0ebc5d3e-170e-40cf-85b4-e72e38851071" />



Rest all are component level and @vinutv will be updating


Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Navigation**
  * Patient search now has a dedicated link, separate from the Encounters section and its related pages.
* **Usability**
  * The sidebar returns to the top when switching between sidebar sections or facility settings.
  * Keyboard shortcuts remain available when the shortcut command dialog is open, even if other dialogs are present.
* **Visual Improvements**
  * Updated the layout and spacing of clinical history pages and the schedule template sheet.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e596835a5b36`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.