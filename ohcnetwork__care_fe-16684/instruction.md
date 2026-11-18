# Issue

**Title:** [ENG-914] Fix local dev plugin discovery

## Description

## Proposed Changes

Fixes https://openhealthcarenetwork.atlassian.net/browse/ENG-914

- Fix local plugin discovery by supporting multiple manifest file formats
- Update documentation to reflect changes in manifest file paths for local plugin apps, allowing both `manifest.ts` and `manifest.tsx` files. This improves flexibility in plugin configuration and ensures accurate loading in host development mode.

Found while working on https://openhealthcarenetwork.atlassian.net/browse/DOC-31


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
## Summary by CodeRabbit

* **New Features**
  * Local plugin discovery now recognizes manifest files across supported TypeScript and JavaScript extensions, including `.ts`, `.tsx`, `.js`, `.jsx`, `.mjs`, `.mts`, `.cjs`, and `.cts`.
  * Changes to supported manifest formats are detected automatically during development.
  * Discovered plugins continue loading through the host development environment.

* **Documentation**
  * Updated local development and architecture guidance to describe the expanded manifest support.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7271742b4d8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.