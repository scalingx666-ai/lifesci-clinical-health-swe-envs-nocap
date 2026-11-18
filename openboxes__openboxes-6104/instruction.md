# Issue

**Title:** OBPIH-7893 p2. Add DefaultTypeFormatter and base Formatter

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-7893

**Description:** part 2 of  Refactor the formatters to extend from a base Formatter, and add a DefaultTypeFormatter that we will use for formatting date fields in the exporter

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3f6f4bb6f2f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.