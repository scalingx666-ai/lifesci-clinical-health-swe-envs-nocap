# Issue

**Title:** feat(ipmo): Add Stop Medication Order flow for Inpatient Medication Order (backport #1225)

## Description

Issue Description
  Inpatient Medication Order currently does not support stopping only the remaining pending medication doses after some
  doses have already been administered.

  Example: a doctor prescribes medication for 2 days with 3 doses per day. If Day 1 doses are already administered and
  the doctor changes the treatment plan, staff need to stop only the pending Day 2 doses. Cancelling or stopping the
  whole medication order is not suitable because completed/administered medication history must remain unchanged.

  Fix Applied
  Added a Stop Medication Order action on submitted IPMO documents. Users can select pending medication schedule rows,
  enter a mandatory stop reason, and mark only those rows as Stopped. Completed rows remain unchanged, stopped rows are
  excluded from future IPME creation, and parent IPMO status is recalculated based on remaining pending rows.

  File-Wise Changes
1.inpatient_medication_order.py

  - Added server method stop_medication_orders.
  - Validates IPMO is submitted.
  - Requires at least one selected row and mandatory stop reason.
  - Checks selected rows still belong to the IPMO.
  - Blocks stale rows that are no longer Pending.
  - Updates selected child rows to Stopped with stop_reason.
  - Recalculates parent status using pending child rows.
  - Keeps completed_orders based only on Completed rows.

2. inpatient_medication_order.js

  - Added Stop Medication Order button for submitted IPMOs.
  - Opens an extra-large dialog showing only pending medication rows.
  - Uses built-in table row checkboxes for selection.
  - Requires stop reason.
  - Calls server method and reloads the IPMO after successful stop.

3. inpatient_medication_order_entry.json

  - Added Stopped as a supported child row status.
  - Added read-only stop_reason field.

4. inpatient_medication_entry.py

  - Existing IPME validation now blocks stopped rows because only Pending rows are valid.
  - Added helper to detect stopped medication rows inside draft IPME.
  - Added cleanup method to remove stopped rows from draft IPME.
  - Reorders remaining child rows by resetting idx.
  - Added module-level cleanup method to avoid stale client-side document merge issues.

5. inpatient_medication_entry.js

  - On draft IPME refresh, checks whether any rows reference stopped IPMO child rows.
  - Shows frappe.confirm asking user to remove stopped rows.
  - If confirmed, removes stopped rows from server and visible grid.
  - Reorders visible row numbers and reloads the document.

6. test_inpatient_medication_order.py

  - Added tests for stopping pending rows after partial completion.
  - Added stale row validation test.
  - Added draft IPME stopped-row cleanup test.
  - Added row reordering test after removing stopped rows.

Images:-
1.IPMO with Stop Medication Order Button
<img width="1675" height="771" alt="image" src="https://github.com/user-attachments/assets/d976d419-9283-4b70-bdbf-02f8e32cc6d3" />
<img width="1173" height="822" alt="image" src="https://github.com/user-attachments/assets/261a132d-f227-447b-b7d9-3a11f82c8791" />

2. after stop 2 rows
<img width="1537" height="819" alt="image" src="https://github.com/user-attachments/assets/631356ea-929b-4a16-8346-9b4b73773ca4" />

3.Confirmation Popup in IPME
<img width="1531" height="864" alt="image" src="https://github.com/user-attachments/assets/97aa88f3-6366-4871-b6af-0620cf027364" />

  Steps To Test

  1. Create and submit an Inpatient Medication Order.
  2. Add medication schedule for 2 days with multiple doses per day.
  4. Create an Inpatient Medication Entry for Day 1 pending rows.
  5. Submit the IPME.
  6. Confirm Day 1 IPMO child rows become Completed.
  7. Open the submitted IPMO.
  8. Click Stop Medication Order.
  9. Confirm the dialog shows only Pending rows.
  10. Select one or more pending rows using the table checkboxes.
  11. Enter a stop reason.
  12. Click Stop.
  13. Confirm selected rows become Stopped.
  14. Confirm completed/administered rows remain Completed.
  15. Confirm stop_reason is saved on stopped rows.
  16. Confirm parent IPMO status updates:
      - Pending if all rows are pending.
      - In Process if some rows are still pending.
      - Completed if no pending rows remain.

  17. Create a new IPME for the same filters/date.
  18. Confirm stopped rows are not fetched.

  Draft IPME Cleanup Test

  1. Create a draft IPME containing pending medication rows.
  2. Open the related IPMO.
  3. Stop one or more of those pending rows.
  4. Reopen or refresh the draft IPME.
  5. Confirm a popup appears asking to remove stopped rows.
  6. Click Yes.
  7. Confirm stopped rows are removed.
  8. Confirm remaining rows are renumbered correctly.
  9. Confirm saving/submitting is blocked if stopped rows are still present and the user does not remove them.

Inpatient Medication Order Report Changes:-
    - Updated Inpatient Medication Orders report to use child row status instead of old is_completed logic for pending
      filtering.
    - Added Status and Stop Reason columns to the report.
    - Updated chart counts to use Pending, Transferred, Completed, and Stopped.
    - Renamed filter label from Show Completed Orders to Show All Orders because checked now shows all statuses, not
  only
      completed rows.
    - Updated Pending IP Medications number card to count only rows with status = "Pending".
    - Added tests to confirm stopped rows do not appear in pending report results and still show with stop reason when
  all
      rows are shown.

Why:
    - Stopped rows keep is_completed = 0, so old report logic treated them as pending.
    - The report needed to follow the new status-based medication flow.

<img width="1658" height="950" alt="image" src="https://github.com/user-attachments/assets/d5f18504-d64c-4ceb-b373-25b88183ea83" />

no-docs

<hr>This is an automatic backport of pull request #1225 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `89f9945346d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.