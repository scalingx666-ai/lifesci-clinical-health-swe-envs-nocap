# Issue

**Title:** [ENG-1169] fix: update shortcut IDs for keyboard actions for charge Item

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/152/changes/care_fe/152
<!-- entire-trail-link-end -->

## Proposed Changes

Fixes ENG-1169
- Here the shortcut was not working will for "Add charges. Press Enter to start searching."
<img width="1212" height="824" alt="image" src="https://github.com/user-attachments/assets/f5d0e4e1-f399-412c-a486-2b382674313c" />

- Here both "Add charges. Press Enter to start searching." and submit shortcut
<img width="1212" height="824" alt="image" src="https://github.com/user-attachments/assets/0ebc5d3e-170e-40cf-85b4-e72e38851071" />

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0fbf6113fd21`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.