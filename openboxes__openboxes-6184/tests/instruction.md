# Issue

**Title:** OBPIH-7984 styling on receipt item table

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-7984

**Description:** Three changes:
1) Make borders thicker on table views (1px -> 2px)
2) Vertical stripe only shows red for errors, otherwise is hidden
3) Hide dotted separator between the dropdown "X changes applied" row and the first split row if the original row has the same product as the split row


---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

<img width="1858" height="605" alt="Screenshot from 2026-09-21 13-55-15" src="https://github.com/user-attachments/assets/ff41b95f-2cd8-4277-a093-7878cdae7b20" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b500f168d7a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.