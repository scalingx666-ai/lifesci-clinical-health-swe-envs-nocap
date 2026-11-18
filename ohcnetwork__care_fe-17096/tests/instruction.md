# Issue

**Title:** [ENG-1204] 🗂️ Fix NaN offset in files list pagination

## Description

## Proposed Changes

- ENG-1204

The Files tab (encounter and patient) sent `offset=NaN` and no `limit` to `GET /api/v1/files/`, so pagination was broken. The page size was read from `qParams.limit`, which is not in the URL on first load or after a page change.

- Use `resultsPerPage` from `useFilters` for `limit` and `offset` in `FileSubTab`. This fixes the encounter and patient Files tabs, which share this component. Other file lists use `query.paginated` or send no offset, and are not affected.
- Add `tests/facility/patient/encounter/files/encounterFilesPagination.spec.ts`. It creates 16 encounter files through the API (create + `mark_upload_completed`, so no file storage is needed), then asserts:
  - page 1 sends `limit=15&offset=0`, page 2 sends `limit=15&offset=15`
  - page 2 shows different files than page 1
  - every files list request sends a numeric `offset`

Validation (local backend):
- `npx playwright test tests/facility/patient/encounter/files/` with the fix: passed.
- Same test without the fix: failed (`limit` missing from the request).
- `tests/facility/patient/patientDetails/files/patientFiles.spec.ts`: 4 failed locally because file storage (`localhost:7070`) was not running. Not related to this change.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Fixed encounter-file pagination so each page displays the correct set of files and advances by the expected number of results.
  * Page navigation now uses the selected page size consistently, helping prevent files from being repeated or skipped between pages.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57205b897804`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.