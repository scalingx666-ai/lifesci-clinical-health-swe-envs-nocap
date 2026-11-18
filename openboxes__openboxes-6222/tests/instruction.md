# Issue

**Title:** OBPIH-7944 Show received columns on receiving step and update status preview on cancel remaining

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:**
https://pihemr.atlassian.net/browse/OBPIH-7944

**Description:**
  I made the changes Kelsey asked for in her comments under this ticket:

  - The Received and To Receive columns now show on the receiving page when there was a previous receipt.
  - The shipment status now updates live when you check or uncheck Cancel Remaining.



---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `573af8c1848b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.