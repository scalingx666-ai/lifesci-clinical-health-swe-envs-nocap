# Issue

**Title:** OBPIH-8001 pt2. bulk inventory item create

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-8001

**Description:** In the receiving edit modal, if you split a product into two rows with the same new lot, it would error on the second because it tried to insert both. We now collect duplicates properly ahead of time and only create them once.


---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

https://jam.dev/c/a77f8533-7b6f-4dec-b3c7-c0e47e0274ca

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b477674a4a6f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.