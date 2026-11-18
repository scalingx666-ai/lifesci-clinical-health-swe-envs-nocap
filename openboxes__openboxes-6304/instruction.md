# Issue

**Title:** OBPIH-7763 Fix bin replenishment table

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-7763?atlOrigin=eyJpIjoiZjQyYWNiN2RmZjhiNDcxNDg5ZDU0M2Y1ZmM4ZTAyZTEiLCJwIjoiaiJ9

**Description:**
- Fixed the crash in ArrayField tables (bin replenishment, stock movement wizards, returns, invoices, put-away): the row tooltip no longer translates an undefined validation error

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1acdf7694464`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.