# Issue

**Title:** [ENG-635] feat: Add password reset via OTP

## Description

## Proposed Changes

Fixes https://openhealthcarenetwork.atlassian.net/browse/ENG-635
- Wire password reset via phone number -> OTP 
- Move the common elements between email reset and otp reset into a shared component
- Add required  playwright tests


https://github.com/user-attachments/assets/9c0d1ccf-6d2a-4008-950a-6e6ce2849abb



Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added phone-based password reset with OTP, including OTP confirmation, resend countdown, and new-password setup.
* **Improvements**
  * Unified the forgot-password experience across login and reset flows with consistent two-step UI and validation.
  * Enhanced the UI for shared-phone scenarios by requesting a username when required.
  * Expanded English localization for email and phone reset messaging.
* **Bug Fixes**
  * Improved handling and display of invalid OTP and server-returned reset errors.
* **Tests**
  * Added end-to-end coverage for OTP reset success, invalid OTP, and unknown-phone scenarios.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c560786221c6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.