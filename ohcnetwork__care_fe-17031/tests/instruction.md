# Issue

**Title:** [ENG-1130] Fix broken links on finished queue list

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/153/changes/care_fe/153
<!-- entire-trail-link-end -->

## Proposed Changes

ENG-1130

- Fixes broken links on finished queue list

Tagging: @ohcnetwork/care-fe-code-reviewers

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
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Patient and encounter links in the finished-queue desktop table and mobile cards now navigate from the application’s root path. Their destinations remain unchanged, preserving the existing facility, queue, and encounter details.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `81e7515fdf4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.