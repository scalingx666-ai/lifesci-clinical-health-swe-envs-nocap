# Issue

**Title:** [QA-365]: Fix outdated playwright tests

## Description

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

* **Updates**
  * Token category resource types can still be selected during creation but are locked when editing an existing category.
* **Bug Fixes**
  * Enter and Space presses on diagnostic report headers no longer trigger parent keyboard interactions.
* **Tests**
  * Updated encounter and diagnostic-report checks to reflect current creation, review, and status workflows.
  * Added coverage confirming token category resource types cannot be changed after creation.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e5ddbb04ebb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.