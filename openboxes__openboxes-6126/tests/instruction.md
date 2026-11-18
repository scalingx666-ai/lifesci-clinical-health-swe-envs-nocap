# Issue

**Title:** OBLS-825 OBLS-838 Assign location to splitted putaway task not to canceled original task

## Description

modify location for all status except COMPLETED and CANCELED

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-825
https://openboxes.atlassian.net/browse/OBLS-838

**Description:**


---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61ba6a0b51a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.