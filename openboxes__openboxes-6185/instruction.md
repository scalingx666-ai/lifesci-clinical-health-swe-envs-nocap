# Issue

**Title:** OBPIH-8018 Hide 0 qty receipt items on SM packing list tab

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-8018

**Description:** In V2 receiving we still create receipt items even if we are receiving and canceling 0 quantity. To preserve existing behaviour, we need to filter out those zero quantity rows from the packing list tab on the stock movement view page.

Also moved bin location to a different column as requested in the ticket.


---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

Splitting a product into another product while still receiving some quantity on the original product:
<img width="1618" height="294" alt="Screenshot from 2026-09-22 12-09-45" src="https://github.com/user-attachments/assets/21151183-52eb-4d30-af3e-b64b9609657c" />

Shows both rows on the packing list view:
<img width="1424" height="146" alt="Screenshot from 2026-09-22 12-10-07" src="https://github.com/user-attachments/assets/890a9a10-5e17-4926-b1e7-9f1664e46b09" />

Splitting a product into another product and receiving 0 quantity on the original product:
<img width="1575" height="241" alt="Screenshot from 2026-09-22 12-05-01" src="https://github.com/user-attachments/assets/3dbbe59d-429b-420a-a2d0-b46aab71d2d5" />

Shows only the split row on the packing list view:
<img width="1440" height="164" alt="Screenshot from 2026-09-22 12-05-25" src="https://github.com/user-attachments/assets/036f7ae4-b570-49ab-ab02-89d1cd35429c" />

Note that in both scenarios the lot, bin, and recipient info for the split row appears under the original product, even though the split row is for a different product. This is pre-existing behaviour and is not being resolved in the ticket.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b500f168d7a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.