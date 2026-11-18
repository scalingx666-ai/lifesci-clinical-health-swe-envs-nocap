# Issue

**Title:** [ENG-1106] Add inventory usage configuration for locations

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/110
<!-- entire-trail-link-end -->

## Proposed Changes

Locations can now be configured with the `inventory_usage` field introduced in . The create/edit form supports None, Store, Supplier, Consumption, and Adjustment, defaults new locations to None, and restores the saved selection when editing.

- Preserve the selection during unrelated edits and allow explicitly resetting it to None.
- Apply the selected usage to every bed created in bulk; CSV imports continue to default to None without changing the CSV layout.
- Add typed read/write support and English translations. Writes may omit the field to preserve the backend’s update semantics.

## Validation

- `npx tsc --noEmit` — passed.
- `npm run build` — passed.
- `npm run lint` — passed with 394 warnings and no errors; targeted ESLint and Prettier checks passed.
- Playwright against an isolated local backend at the linked commit: 8 existing location creation/edit tests and 2 new inventory usage tests passed, plus authentication/facility setup.
- Desktop and mobile viewport previews checked.

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update product documentation.
- [x] Ensure that UI text is placed in I18n files.
- [ ] Attach a screenshot or demo video for the changelog entry.
- [ ] Request peer reviews.
- [x] Complete QA on mobile devices (browser viewport).
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes.

## Jira

- Engineering: [ENG-1106](https://openhealthcarenetwork.atlassian.net/browse/ENG-1106)
- Core story: [CARE-403](https://openhealthcarenetwork.atlassian.net/browse/CARE-403)
- Feedback source: [CIMPL-300](https://openhealthcarenetwork.atlassian.net/browse/CIMPL-300)

[ENG-1106]: https://openhealthcarenetwork.atlassian.net/browse/ENG-1106?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60f49fb358cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.