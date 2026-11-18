# Issue

**Title:** [ENG-1030] Fix Care Reviewer gh-aw

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/15
<!-- entire-trail-link-end -->


## Proposed Changes

Fixes https://openhealthcarenetwork.atlassian.net/browse/ENG-1030
- Fixes concurrency issue, earlier review jobs getting cancelled because of other events happening on the PR, especially happening when PR is opened
- Fixes reply to review comments on the fork branches


> [!NOTE]
> Tested every flow here 
>   




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

- **New Features**
  - Added automated replies to supported CARE review threads and direct mentions on forked pull requests.
  - Can resolve review threads when a finding is confirmed to be incorrect or its fix is verified.
  - Reports when a required review tool is unavailable.
- **Improvements**
  - Skips bot comments, unrelated comments, and review comments on pull requests from other repositories.
  - Verifies that comments belong to the expected pull request before processing.
  - Separates comment runs from review runs to reduce duplicate processing and avoid canceling unrelated work.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83b007b72cd0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.