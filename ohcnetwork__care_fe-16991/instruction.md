# Issue

**Title:** [ENG-1129] Added search bar in service list page

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/120/changes/care_fe/120
<!-- entire-trail-link-end -->

## Proposed Changes

Adds a search bar in the service list page

<img width="1162" height="323" alt="image" src="https://github.com/user-attachments/assets/5ecd6351-d3d2-4c21-9a9f-ae85f2f6c586" />


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
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

- **New Features**
  - Added a search field to the healthcare services page.
  - Service results can now be filtered by name using the entered search term.
  - Search input includes a localized label, placeholder, and search icon.
  - Search criteria are reflected in the page URL for easier navigation and sharing.
  - Clearing the field removes the active search filter.
  - Starting a search from a later results page now returns users to the first page.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8ac63ec0d595`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.