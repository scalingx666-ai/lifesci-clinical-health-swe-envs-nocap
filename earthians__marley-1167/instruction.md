# Issue

**Title:** fix(healthcare): pass uom and qty to healthcare service price lookup (backport #1164)

## Description

Issue description:

Healthcare Service items added through Sales Invoice -> Get Items From -> Healthcare Services were being inserted with zero rate even though valid Item Price records existed.

The custom pricing call to get_item_details() did not include the full pricing context required for these items.

Fix applied:

- Updated set_healthcare_services to fetch the item stock UOM and pass both uom and qty = 1 into ItemDetailsCtx before calling get_item_details().

- This preserves the existing invoice row quantity behavior while allowing ERPNext to match the correct Item Price and populate the proper rate.

Test Case After Fix:
1. Go to Sales Invoice.
2. Select the patient, customer will be autofetch.
3. Click on Get Items From -> Healthcare Services.
4. Select the items and click on Add button.
5. Items will be inserted to sales invoice item table with proper qty and rates.
6. If step 5 is successful, then the test case is passed.

Closes issue: #1140 <hr>This is an automatic backport of pull request #1164 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e766c6911462`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.