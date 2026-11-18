# Issue

**Title:** [QA-210] Allow QA project key in PR title JIRA validation

## Description

## Proposed Changes

The `PR Title JIRA Validation` workflow (`.github/workflows/pr-title-jira.yml`) only allowed the `ENG` project key. PRs referencing valid QA-project tickets (e.g. [QA-32] in #16317) fail the check because `QA` is not recognized.

This adds `QA` to the allowed `jiraProjectKeys` list so titles like `[QA-123] ...` pass validation.

- Fixes the failing JIRA validation on #16317

Ref: QA-210

[QA-32]: https://openhealthcarenetwork.atlassian.net/browse/QA-32?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ
[QA-123]: https://openhealthcarenetwork.atlassian.net/browse/QA-123?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * Updated pull request title validation to accept titles beginning with either an ENG or QA JIRA issue key.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd3299d27f4a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.