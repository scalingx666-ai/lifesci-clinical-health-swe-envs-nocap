# Issue

**Title:** [ENG-1173] fix: TextArea size issue in Appointment

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/154/changes/care_fe/154
<!-- entire-trail-link-end -->

## Proposed Changes

Fixes ENG-1173

- Fix not the note layout issue in the appointment schedule, cancel, etc. 
before
<img width="1040" height="637" alt="image" src="https://github.com/user-attachments/assets/336359cc-712c-426e-9ac7-546cb60341c2" />

after
<img width="1040" height="637" alt="image" src="https://github.com/user-attachments/assets/4bc02f79-512b-4ec7-8bf0-5cb5b7274014" />



Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f09cd206775d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.