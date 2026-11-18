# Issue

**Title:** OBPIH-7966 Layout improvements in the edit line item modal

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:**
https://pihemr.atlassian.net/browse/OBPIH-7966

**Description:**
No bin location support, shipment not from a PO
<img width="2491" height="1316" alt="image" src="https://github.com/user-attachments/assets/b6b4e9af-4f91-4e12-8ad9-aa3a8b3a0cf6" />

Bin location support, shipment not from a PO:
<img width="2491" height="1316" alt="image" src="https://github.com/user-attachments/assets/e59fbeac-eff8-400e-94d3-5435f026f1e5" />

No bin location support, shipment from a PO:
<img width="2491" height="1316" alt="image" src="https://github.com/user-attachments/assets/61f1bd8e-2bf4-4116-a002-6f484177346d" />

Bin location support, shipment from a PO:
<img width="2491" height="1316" alt="image" src="https://github.com/user-attachments/assets/bf20aa62-4ec4-4e35-acca-703ae5ce9832" />
  

---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `774f28976eaa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.