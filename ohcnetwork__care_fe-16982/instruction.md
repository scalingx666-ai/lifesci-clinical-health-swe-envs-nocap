# Issue

**Title:** [ENG-1112] fix: simplify purchase price calculation in useDeliveryRowItem hook

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/113
<!-- entire-trail-link-end -->

## Proposed Changes

Fixes ENG-1112

<img width="888" height="251" alt="image" src="https://github.com/user-attachments/assets/442a8ff6-67f1-455d-8ec4-83f459550cf8" />

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **Bug Fixes**
  - Corrected delivery item purchase price calculations for existing products: the automatic total now uses the product’s purchase price multiplied by pack size.
  - When entering a total purchase price, the price per pack is now calculated by dividing the total by pack size, provided pack size and pack quantity are valid positive integers. Changing pack quantity alone no longer changes the entered per-pack price.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eed3ad88996e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.