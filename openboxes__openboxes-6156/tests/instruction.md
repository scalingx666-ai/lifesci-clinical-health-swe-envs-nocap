# Issue

**Title:** OBPIH-7997 fix. Add product code back to product select

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-7997

**Description:**  Properly override labelKey to be falsy for product select so that it defaults to the behaviour in ProductSelect.


---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

before fix:
<img width="1024" height="478" alt="image" src="https://github.com/user-attachments/assets/580b43bc-c4f7-4f8b-a66c-180e97d14112" />

after fix:
<img width="467" height="582" alt="image" src="https://github.com/user-attachments/assets/6eefc8ce-ff15-46df-bbcd-eb250a9cfaaf" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6158b540e047`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.