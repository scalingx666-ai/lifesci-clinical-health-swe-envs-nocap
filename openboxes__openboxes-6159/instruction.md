# Issue

**Title:** OBPIH-7996: fix margins on receiving buttons and other changes

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-7996

**Description:** Various changes:

1) Hide import button
2) Change text on “Enable Putaway” slider to “Show Putaway”
3) Add margin around next button on receiving
4) Add margin around save button on modal
5) Add margin around complete and back buttons on check page

---
### :camera: Screenshots & Recordings (optional)

See ticket for original screenshots. Here are screenshots with the change:

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

<img width="1863" height="654" alt="image" src="https://github.com/user-attachments/assets/ce6fb51f-7f1c-432d-ba1f-f5892451657a" />

<img width="1553" height="794" alt="image" src="https://github.com/user-attachments/assets/727c146d-7e97-4466-bbb8-61dff93184ca" />


<img width="1891" height="199" alt="image" src="https://github.com/user-attachments/assets/4adb6e4e-3b7c-45f3-a935-ec342b33afe7" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6158b540e047`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.