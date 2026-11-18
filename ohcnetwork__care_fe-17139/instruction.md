# Issue

**Title:** [ENG-1093] Improve Token Category list UI and restrict resource type edit

## Description

Entire-Checkpoint: 7bb803678cdd

ENG-1093

## Proposed Changes

- Backend no longer supports editing resource type of a token category, hence reflected the same changes in FE.
- Updated token category list UI to match with the 3.1's design system.

<img width="1712" height="1345" alt="image" src="https://github.com/user-attachments/assets/1201d17e-3bde-4fac-bb01-04bc9a7904aa" />

<img width="1712" height="1345" alt="image" src="https://github.com/user-attachments/assets/2bf1fab4-6e20-4543-958b-221ddbe209dc" />

<img width="381" height="668" alt="image" src="https://github.com/user-attachments/assets/f5d2a738-55fa-44d3-bbbf-cf6b03fc610b" />

<img width="388" height="680" alt="image" src="https://github.com/user-attachments/assets/7d8c9aae-72ab-4d2a-860e-6d83192d4d27" />

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [x] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c8a165a8d1b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.