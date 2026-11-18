# Issue

**Title:** Use existing atomic batch API for immunization policy doses

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/133/changes/care_fe/133
<!-- entire-trail-link-end -->

## Proposed Changes

Applying an immunization policy depended on the new `create_tree` backend endpoint. Use the existing batch API to create all dose recommendations in one atomic transaction, preserving the previewed dates and dose metadata while omitting group records. Policies above the existing 20-request limit are blocked before any write.

Remove the frontend's `expected_status` draft-completion field and the CI/setup dependency on care#3809. Resumed drafts still complete through the existing API in the same batch as their responses. Restore the prior ENG-737 backend selection.

Validation: production build, TypeScript, ESLint (0 errors; existing warnings), 20 focused unit tests, and 13 Chromium tests passed. The browser checks use the backend revision before care#3809 and prove persisted 20-dose creation, rejection above the limit, rollback after a later dose fails, and retry without duplicates. The new limit regression test failed against the previous frontend build as expected. Independent code review found no implementation issues.

The browser run reused an existing seeded database. This does not validate clean CI fixture setup; missing questionnaire fixtures remain a separate backend/setup issue. No backend source or remote changes are included.

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a42f0fa2b362`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.