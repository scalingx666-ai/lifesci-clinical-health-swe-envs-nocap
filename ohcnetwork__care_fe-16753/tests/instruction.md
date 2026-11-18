# Issue

**Title:** [ENG-975] feat: add loading cover to appointment print

## Description

fixes: ENG-975

Just adding a cover FOR LOADING

<img width="878" height="822" alt="image" src="https://github.com/user-attachments/assets/b3d4a62a-e5f7-4f5c-a8ce-ebfa317154dc" />



Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Improved appointment printing with a loading indicator while charge and invoice details are retrieved.
  * Print preview is temporarily disabled until all required billing information has loaded.
  * Preserved appointment, patient, billing, payment, notes, QR code, and footer details in printed output.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a578b5a4c32d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.