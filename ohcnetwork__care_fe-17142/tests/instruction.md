# Issue

**Title:** [ENG-1233] Fix the data stale issue because of query fetch getting cancelled

## Description

## Proposed Changes

Fixes https://openhealthcarenetwork.atlassian.net/browse/ENG-1233

> Changelog Video

https://www.loom.com/share/8d2e9cca0c024b6cb8538a785ce7f844

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

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbdbe79e0b70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.