# Issue

**Title:** fix(observation): stale Sales Invoice Status on Observation records (backport #1066)

## Description

Issue description:
When an Observation is linked to a Sales Invoice, the Sales Invoice Status field can incorrectly remain Unpaid even after the invoice has been paid.
This happens because the field was defined with:
                      fetch_from: "sales_invoice.status"

Due to this, the invoice status was stored on the Observation record. If the Sales Invoice status changed later through payment processing, the Observation field did not refresh automatically.

Before fix:

<img width="686" height="247" alt="image" src="https://github.com/user-attachments/assets/1628bbb8-ac4b-4116-ad63-849e0da0d0e5" />

Fix:
The fix changes Observation.sales_invoice_status to a virtual live field(is_virtual).
  - Removed fetch_from from the Observation DocType JSON.
  - Added sales_invoice_status as a property in the Observation Python class.
  - The field now reads the current status directly from the linked Sales Invoice.
  - This keeps the Observation aligned with the actual Sales Invoice payment state.

Test after fix:
Make sure Create Observation on Sales Invoice Submission is enabled in Healthcare Settings.
Test the following scenario:
  1. Create an Observation Template and link the billable Lab Service Item to it.
  2. Create a Sales Invoice for a patient.
  3. Add the Lab Service Item to the Sales Invoice.
  4. Submit the Sales Invoice.
  5. Check the created Observation.

Expected result:
  - If the Sales Invoice is only submitted and not paid, the Observation should show the Sales Invoice Status as Unpaid.
  - After creating the Payment Entry and paying the Sales Invoice, the Observation should show the Sales Invoice Status as Paid.

This confirms that the Observation is now showing the live Sales Invoice payment status instead of a stale stored value.

<img width="789" height="272" alt="image" src="https://github.com/user-attachments/assets/4a1be27e-6a88-44d0-8ce1-2d0e292033db" />

Note:-
After pulling the changes , run bench --site sitename migrate to reflect the changes.<hr>This is an automatic backport of pull request #1066 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8bfb69b79578`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.