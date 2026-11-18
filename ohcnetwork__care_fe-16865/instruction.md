# Issue

**Title:** [ENG-1051] feat: update selectable encounter statuses logic in EncounterQuestion component

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/44
<!-- entire-trail-link-end -->

fixes: ENG-1051
Entire-Checkpoint: 833f9ada9ffc

## Proposed Changes
Allow change encounter status to in-progress if discharged.


<img width="1148" height="489" alt="image" src="https://github.com/user-attachments/assets/77bc97f5-2762-4735-a779-ed766d45291c" />


Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Discharged encounters can now be moved back to in progress. The status selector remains available unless explicitly disabled.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01f5480cb6c6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.