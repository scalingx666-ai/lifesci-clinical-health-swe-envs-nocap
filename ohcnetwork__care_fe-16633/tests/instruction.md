# Issue

**Title:** Adding secondary reviewer for care fe

## Description

## Proposed Changes

- Repurposing loopd reviewer and adding it as a workflow for FE

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
  * Added automated pull request reviews for code clarity, simplicity, accessibility, responsive behavior, and user experience.
  * Reviews support initial checks, follow-up reviews, and responses to relevant comments and discussions.
  * Added duplicate-finding prevention and verification of previous review findings.

* **Chores**
  * Added secure review execution with result tracking, usage limits, and status reporting.
  * Added configurable frontend review guidance and concise, consistent feedback standards.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f148f3183691`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.