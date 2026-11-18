# Issue

**Title:** OBPIH-8050 Disable receiving when logged into different location

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:**

**Description:**
I'm leaving this for review, but I don't like one case which I would like to discuss with Kuba - if you change the location on the check step, change the location, come back to the first step, the sync endpoint would fail, so we won't return a receipt. Moreover, the receipt is never re-fetched when you switch the location, so we end up with an empty table and we are forced to refresh the page for that scenario:
<img width="2533" height="751" alt="Screenshot From 2026-10-19 20-46-05" src="https://github.com/user-attachments/assets/4b621e12-3147-4081-98df-1c5b8d9b5ff1" />

I will try to find out if it can break any autosave logic if we were to refetch the receipt when we are switching the locations back and forth.

---
### :camera: Screenshots & Recordings (optional)
<img width="2533" height="751" alt="Screenshot From 2026-10-19 20-25-51" src="https://github.com/user-attachments/assets/d660c2e9-1ef8-452a-849c-4ad685ca6457" />
<img width="2533" height="751" alt="Screenshot From 2026-10-19 20-22-44" src="https://github.com/user-attachments/assets/44b079f5-5726-46bb-b035-7d73a4908f54" />

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `727b7d880fcc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.