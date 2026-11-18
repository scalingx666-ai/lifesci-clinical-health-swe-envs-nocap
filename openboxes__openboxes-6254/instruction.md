# Issue

**Title:** OBS-1989 better error message when dateDelivered in future

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBS-1989

**Description:** Show a localized error when delivery date is in the future. This does not solve the underlying issue. It just makes the error message clearer.

---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

The old, unclear error:

https://github.com/user-attachments/assets/db09a864-a834-46e4-9a48-6c0269371611

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4be77f4a69bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.