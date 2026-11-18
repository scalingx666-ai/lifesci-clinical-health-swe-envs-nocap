# Issue

**Title:** [ENG-1023] 🛠️ Fixes origin/destination not synced when location is changed in delivery/request order form

## Description

> [!NOTE]
> JIRA Ticket: **ENG-1023**
> Entire Trail: https://entire.io/gh/ohcnetwork/care_fe/trails/8

## Proposed Changes

- When location is switched from location switcher, the `origin` on Delivery Order, and `destination` on Request Order form states were not updated/synced. This has been fixed.

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

- **Enhancements**
  - New delivery orders now automatically populate location fields based on the selected facility and order type.
  - Internal delivery orders use the facility as the origin, while external orders use it as the destination.
  - New request orders automatically set the facility as the destination.
  - Conflicting origin or destination values are cleared when necessary to keep location details consistent.
  - Existing orders and orders linked to supply orders retain their current location values.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c22b5c208a59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.