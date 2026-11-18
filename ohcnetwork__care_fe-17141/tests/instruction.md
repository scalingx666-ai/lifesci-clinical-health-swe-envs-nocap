# Issue

**Title:** [ENG-1075] feat: add SupplyDeliveryFormActions component type and integrate into AddSupplyDeliveryForm

## Description

## Proposed Changes

Fixes: ENG-1075

<img width="1216" height="569" alt="image" src="https://github.com/user-attachments/assets/eae624cf-d740-44d2-a865-1b1cb0160cd0" />

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
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * External-supply delivery forms can display additional actions provided by installed plugins. These actions have access to the facility, delivery order, and current form details.
  * Origin-based delivery forms do not display these plugin-provided actions.
* **Bug Fixes**
  * Delivery items marked as manually edited are treated as new items, including when that status is set by a plugin. This also ensures category selection reflects the item’s edited status.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e5ddbb04ebb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.