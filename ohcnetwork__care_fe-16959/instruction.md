# Issue

**Title:** [ENG-1078] Add back no account warning when billing new prescriptions

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/94
<!-- entire-trail-link-end -->

## Proposed Changes

- ENG-1078
- Adds warning when billing prescriptions when no account already exists.

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

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added shortcut badges to the no-active-account dialog’s proceed and go-to-accounts actions.
  * The no-active-account warning now appears when billing medications by prescription.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f30bb8647215`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.