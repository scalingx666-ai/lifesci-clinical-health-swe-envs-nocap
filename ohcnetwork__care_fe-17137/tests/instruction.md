# Issue

**Title:** remove unused interpolation of type in "no files found" translation

## Description

## Proposed Changes

- Pass translated lowercase file type `{ type: t(type).toLowerCase() }` to `no_files_found` translation in `FileListTable.tsx` and `FileSubTab.tsx`.
- Resolves the issue where `no_files_found` ("No {{type}} files found") rendered with an unfilled placeholder and double space ("No  files found") when no files were present.
- Now renders "No patient files found", "No encounter files found", or "No diagnostic report files found" across mobile and desktop views.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Empty file lists now display the file type in the “no files found” message across table and card layouts.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c8a165a8d1b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.