# Issue

**Title:** [ENG-790] feat: enhance prescription print

## Description

## Proposed Changes

Fixes ENG-790

Was merged before here: 

<img width="1200" height="1148" alt="image" src="https://github.com/user-attachments/assets/062914e3-f8ae-4905-a129-8e0434e55ffa" />


Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes



<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Enhanced prescription printouts with timestamps, patient details, encounter information, medication notes, QR codes, and multi-prescription labels.
  * Added configurable print footers and improved table layouts with spanning rows and customizable styling.
  * Added translations for hashtags, medicine instructions, patient IP locations, and item counts.

* **Bug Fixes**
  * Improved dosage rounding and display consistency.
  * Refined medication and prescription print formatting.
  * Updated serial-number labels for improved localization.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `038a33ff9de1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.