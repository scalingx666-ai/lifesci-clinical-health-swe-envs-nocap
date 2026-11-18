# Issue

**Title:** [ENG-749] feat: add search functionality for facilities and other in Dashboard and Facility Switcher

## Description

## Proposed Changes

Closed PR 

Related to ENG-749

<img width="1512" height="792" alt="image" src="https://github.com/user-attachments/assets/df8d4ee3-74ea-43f2-82ee-4afcaa78e453" />
<img width="1512" height="792" alt="image" src="https://github.com/user-attachments/assets/d1d38268-413d-48b6-8b6d-a069d98cf5ec" />
<img width="1512" height="792" alt="image" src="https://github.com/user-attachments/assets/5a0a43fc-5fbe-492e-8182-48ec24bd737f" />


<img width="2124" height="821" alt="image" src="https://github.com/user-attachments/assets/c884080f-7f42-4f06-9ff7-bd4c496ee3fb" />
<img width="2124" height="821" alt="image" src="https://github.com/user-attachments/assets/72c778d4-93f7-4f0e-b0d0-bf207ca69f97" />


Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

## New Features

- Added case-insensitive facility search in the facility switcher.
- Added searchable filtering for dashboard facilities and responsibilities.
- Displays clear empty states when no matches are found.
- Search fields appear when multiple items are available and reset after selection or closing.
- Improved accessibility with a labeled facility selector.
- Dashboard tabs now support horizontal scrolling.

## Improvements

- Updated landing page search labels for clearer facility-search wording.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `038a33ff9de1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.