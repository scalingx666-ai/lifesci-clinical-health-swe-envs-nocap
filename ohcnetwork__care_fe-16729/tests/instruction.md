# Issue

**Title:** [ENG-950] Skip setting `dispense_status` when creating medication requests

## Description

## Proposed Changes

- Skip setting `dispense_status` when creating medication requests

ENG-950

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [x] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Medication requests created from templates or converted from historical medication records now leave the dispense status unset until it is explicitly determined.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d49910962477`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.