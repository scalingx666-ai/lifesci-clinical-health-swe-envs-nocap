# Issue

**Title:** OBLS-946 Unexpected putaway task created when perform more than 2 splits in putaway

## Description

avoid changing older putaway task CANCELLED->PENDING, keep then CANCELLED

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-946

**Description:**
The reason was quite interesting. No new putaway task was created, but a CANCELED putaway task from two splits behind was changed back to PENDING.

So the 3rd split changed back the CANCELED task from the 1st split. The 4th split changed back the CANCELED task from the 2nd split. And so on.

Hopefully now it’s fixed.

---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d7dfc4b40847`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.