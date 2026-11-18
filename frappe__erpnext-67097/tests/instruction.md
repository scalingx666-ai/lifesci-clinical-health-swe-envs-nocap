# Issue

**Title:** fix(stock): refuse a Company that is not text in the Pick List queries

## Description

`check_pick_list_company` (added in #66037) checked the Company only when it was a string. A Company sent as a number skipped the check, and the Pick List query then compared that number with the company names in the database, where a name that starts with the same digits can match. Now a Company that is not text is refused with a validation error, so the Company filter is always checked and compared as text.

**Example:**
- **Setup:** User `stock-b@example.com` has the Stock User role and a User Permission with **Allow** `Company` and **For Value** `Company B`. Company `123 Logistics` has a submitted, open Pick List for a Sales Order of Customer `Grant Plastics`.
- **Steps:**
   1. As that user, call `erpnext.stock.doctype.pick_list.pick_list.get_pick_list_query` with Customer `Grant Plastics` and the Company given as the number `123` instead of the company name.
- **Before the fix:** The company check was skipped, and the user could get the Pick List of `123 Logistics`.
- **After the fix:** The user gets "Company must be text". **Get Items From > Pick List** on Delivery Note sends the Company name as text, so users see the same Pick Lists as before.

**Fix:** In `check_pick_list_company`, throw a validation error when the Company is given but is not a string, before the empty check. ()

**Note for reviewers:** The helper also guards `get_pending_work_orders` and `get_item_details`, so they refuse a Company that is not text too. All three are called from `delivery_note.js` and `pick_list.js` with the Company of the form, which is text, or with no Company (`get_item_details`), which still skips the check as before. The backports of #66037 (#67036 and #67062) have the same follow-up commit.

### How to test

1. Make a submitted Pick List for a Sales Order of `_Test Customer` in `_Test Company`.
2. Open a new Delivery Note for `_Test Company` and `_Test Customer`, and click **Get Items From > Pick List**. The Pick List shows, as before.
3. Call `get_pick_list_query` with the filters `{"company": 123, "customer": "_Test Customer"}`. You get the error "Company must be text".

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f6c7d5b1db85`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.