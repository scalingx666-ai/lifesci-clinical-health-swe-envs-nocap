# Issue

**Title:** OBLS-945 Display stock transfer reason code in ob

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-945

**Description:**
- Stock transfer view page - _\_orderSummary.gsp_
- ~~Stock history tab - _\_showStockHistory.gsp, StockHistoryAssembler.groovy, StockHistoryDisplayContext.groovy, InventoryItemController.groovy_~~
- ~~Transaction details page - _\_entries.gsp_~~
- Email notification - _\_stockTransfer.gsp_
- Generated stock transfer PDF - _\_printPage.gsp_

---
### :camera: Screenshots & Recordings (optional)
<img width="1878" height="857" alt="image" src="https://github.com/user-attachments/assets/23029751-73b6-4ba2-9122-59bdbdf6531e" />
<img width="1278" height="664" alt="image" src="https://github.com/user-attachments/assets/f188427c-eba5-424b-9cab-b0a17189e8e1" />


[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af96a579178b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.