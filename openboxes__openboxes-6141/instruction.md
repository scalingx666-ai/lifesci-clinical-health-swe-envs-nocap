# Issue

**Title:** OBPIH-7997 fix SelectCell all options having focus

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-7997

**Description:** If the user has already selected a location, and opens the location dropdown, the whole dropdown is highlighted.


---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

<img width="513" height="412" alt="image" src="https://github.com/user-attachments/assets/f9ba3d02-4226-4230-9707-ad6ac347280d" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3f654c7a2381`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.