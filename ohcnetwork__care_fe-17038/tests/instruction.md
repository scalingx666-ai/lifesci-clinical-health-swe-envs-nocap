# Issue

**Title:** [ENG-1179] refactor: simplify SearchInput and PhoneInput components

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/159/changes/care_fe/159
<!-- entire-trail-link-end -->

## Proposed Changes

Fixes ENG-1179

- fixed the annoying overflow
<img width="901" height="466" alt="image" src="https://github.com/user-attachments/assets/c38c8e5a-3aa9-4e05-af13-bb65e7632465" />

- updated the active highlight
<img width="901" height="466" alt="image" src="https://github.com/user-attachments/assets/3d36e619-19b0-427b-b61d-e6789964a903" />

- refactored the clear button
<img width="901" height="466" alt="image" src="https://github.com/user-attachments/assets/4c129565-4c73-48bb-8669-24872de36ed8" />

- removed the unwanted ecs key and updated the keyboard shortcuts
<img width="901" height="466" alt="image" src="https://github.com/user-attachments/assets/c4906199-862a-4c17-8d54-38de17c6aae7" />

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3988da363851`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.