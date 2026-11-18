# Issue

**Title:** [ENG-999] fix: multiselct on iPhone and improve styling

## Description

## Proposed Changes
fixes few things missed in 
fixes: ENG-999

**Before**
<img width="360" height="271" alt="image" src="https://github.com/user-attachments/assets/223da7c4-872b-4ca2-ad64-34bd7d465a5c" />
<img width="301" height="556" alt="phone" src="https://github.com/user-attachments/assets/5569c590-787c-4073-bacd-58b9ce34f292" />



**After**
<img width="360" height="271" alt="image" src="https://github.com/user-attachments/assets/57599418-1465-4ea1-b28e-d320071ce7fd" />
<img width="301" height="541" alt="phone" src="https://github.com/user-attachments/assets/ec4d8093-0420-4bc2-8c13-354382a1ac9b" />




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

* **Style**
  * Improved combobox and adjacent button styling for a more seamless appearance.
  * Updated autocomplete clear buttons with gray borders and reduced visual effects.
  * Improved mobile autocomplete text handling to prevent overflow.
  * Added responsive text sizing to multi-select inputs for improved readability across screen sizes.
  * Made mobile drawers more flexible, with 50–85vh height limits.

* **Bug Fixes**
  * Disabled automatic input focus on iOS to provide a smoother mobile experience.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b442bfbd5428`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.