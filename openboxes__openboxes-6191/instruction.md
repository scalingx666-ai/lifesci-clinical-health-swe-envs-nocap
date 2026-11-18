# Issue

**Title:** OBPIH-7957 Fix the receiving table scrolling while there is still empty space below it

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:**
https://pihemr.atlassian.net/browse/OBPIH-7957

**Description:**
How the tables behave on different screens:
https://github.com/user-attachments/assets/3f23098a-a4da-47b4-8b7d-716dc52e69d2
 
1920x1080:
<img width="2189" height="1328" alt="image" src="https://github.com/user-attachments/assets/03979237-b6ab-4d5a-ab16-602572a69ae7" />
<img width="2189" height="1328" alt="image" src="https://github.com/user-attachments/assets/33d4e5ef-155f-4fd9-b30e-f3f74fa1f552" />

1368x768:
<img width="1830" height="974" alt="image" src="https://github.com/user-attachments/assets/5affa1ca-d870-43a7-9d72-5b1c432ccbdd" />
<img width="1830" height="974" alt="image" src="https://github.com/user-attachments/assets/d7f533b4-ca31-486b-a145-a15fca931948" />


---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b500f168d7a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.