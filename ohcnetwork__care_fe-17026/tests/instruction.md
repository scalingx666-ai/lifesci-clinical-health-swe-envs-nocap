# Issue

**Title:** [ENG-1157] Some action fixes 3.1/base

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/149/changes/care_fe/149
<!-- entire-trail-link-end -->

## Proposed Changes

Fixes  https://openhealthcarenetwork.atlassian.net/browse/ENG-1157
- Show the logical operator selector only when there is more than one condition -> **Fixes** Any condition is true (OR) can't be selected
- Add delete confirmation for individual action delete -> **Fixes** Deleting an Action in the questionnaire editor doesn't ask for confirmation
- Improve action summary toast code and style -> **Fixes** The toast says "6 Actions ran" when 2 actions ran 6 instructions and Action toasts turn from blue to white once more than 3 collapse into the summary and The summary toast's layout breaks when its text is short.
  - Replace the `src/Utils/actions/presentActionOutcomes.ts` with `src/Utils/actions/toastActionOutcomes.tsx` 
- Remove the extra add new configuration button in empty state of action list page and also use Empty state component instead of custom one -> **Fixes** The Actions empty state has a second "New Action Configuration" button besides the one at the top right


---

-> Search UI in Action editor is already fixed 
-> On demand run of appointment actions require BE support -> need filters on performable and action_context to reliably and follow common Care FE approach

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Action results now include instruction labels and result counts in notifications.
  * Removing an action requires confirmation, with options to cancel or confirm.
* **Updates**
  * The “Run when” AND/OR selector appears only when an action has multiple conditions.
  * Empty action-configuration lists use a shared empty-state display; the inline create button is no longer shown there.
* **Tests**
  * Added checks for condition-selector visibility and action-removal confirmation.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2cba77aa93c0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.