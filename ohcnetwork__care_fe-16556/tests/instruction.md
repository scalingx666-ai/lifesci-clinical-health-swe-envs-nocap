# Issue

**Title:** [ENG-736] Fix Diagnostic report print is broken in Organization level

## Description

## Proposed Changes

Fix: https://openhealthcarenetwork.atlassian.net/browse/ENG-736

https://github.com/user-attachments/assets/2f9a9014-ab42-4a9f-b4aa-15d62b7287f7


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

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Improved diagnostic report printing by retrieving facility details without interrupting the print preview experience.
  * Preserved existing report loading, PDF/image rendering, and layout behavior.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8160376515fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.