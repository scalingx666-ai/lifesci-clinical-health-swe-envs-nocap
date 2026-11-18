# Issue

**Title:** OBPIH-8002 pt2 - receiving validate lot and expiry control on backend

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-8002

**Description:** The backend equivalent of the lot control checks in  Once that pr is merged these checks should not ever be hit (because they will be caught by the frontend first).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `573af8c1848b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.