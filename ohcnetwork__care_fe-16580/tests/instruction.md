# Issue

**Title:** [ENG-772] Add LOINC code for Oxygen Saturation in Blood in plots

## Description

## Proposed Changes

Adds LOINC code 20564-1 (Oxygen saturation in Blood) to the SpO2 plot config for accurate TeleICU/HMIS vitals plotting

<img width="504" height="443" alt="image" src="https://github.com/user-attachments/assets/0be14784-8275-4b2c-8060-deedfea92ddd" />

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

## Summary by CodeRabbit

* **New Features**
  * Added support for displaying oxygen saturation in blood using the LOINC code `20564-1`.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83d48a04f0cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.