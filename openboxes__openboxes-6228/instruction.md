# Issue

**Title:** OBPIH-8002 pt3. Receiving on inactive bin location

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)
 
**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-8002

**Description:** A missed edge case. Do not allow the submission of a receipt when a receipt item is using a disabled bin location. Only possible if you select the bin location for a row and then disable it after

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61897ec6b962`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.