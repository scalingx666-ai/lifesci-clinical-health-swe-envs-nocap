# Issue

**Title:** OBPIH-7984 fix 2. Don't merge rows when collapsed

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-7984

**Description:** Don't merge the "X changes applied" line with the line below if it is collapsed. This ensures that we always display the solid border between shipment items.


---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)


https://github.com/user-attachments/assets/b36b82eb-8ddd-457f-bc79-e639c2d3760e

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `71454492fd8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.