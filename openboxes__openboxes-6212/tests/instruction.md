# Issue

**Title:** OBPIH-8002 stack2 fail autosave if a row has an invalid value

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-8002

**Description:** Comes from this discussion: 

- The autosave indicator now shows a failure if the row has invalid data
- If you try to save and exit while the autosave still has "dirty" unsaved rows, it warns you that if you proceed they will be lost

---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

Recording (with sound) explaining the new change:

https://github.com/user-attachments/assets/65e782ee-8f9e-471d-a731-ad97cd24c142

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `99bacb4cdd2f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.