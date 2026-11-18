# Issue

**Title:** fix(stock): require Delivery Trip access to show a customer contact in Delivery Trip (backport #65795)

## Description

Backport of #65795 to `version-15-hotfix`. The version-16 backport is #67026.

`get_contact_display` shows the name, phone and mobile number of a Contact. A user without read access on Contact could still get this for any Contact linked to a Customer they can select. Now this fallback also needs read access on Delivery Trip, which is the form that calls the method.

**Fix:** In `check_contact_customer_permission`, also check read permission on Delivery Trip before the Customer select check allows the Contact. ()

**Changes compared with develop:** None. The commit applies without changes. The Delivery Trip route error backport #67055 (of #65792) also changes `delivery_trip.py` and `test_delivery_trip.py`, in other functions. Each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_contact_display_needs_delivery_trip_access`: passes on this branch, fails on `version-15-hotfix` without the fix (no permission error for the Projects User).
- `test_delivery_trip.py` (complete file): 25 of 26 tests pass. `test_delivery_trip_notify_customers` fails on this branch and on `version-15-hotfix` with the same error, because the local test site has no default outgoing Email Account.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.