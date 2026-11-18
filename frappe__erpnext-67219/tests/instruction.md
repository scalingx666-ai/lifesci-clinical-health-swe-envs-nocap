# Issue

**Title:** fix(stock): check Delivery Note read permission before notifying customers from Delivery Trip (backport #65797)

## Description

Backport of #65797 to `version-16-hotfix`.

**Notify Customers via Email** on a Delivery Trip sends each stop's Delivery Note items in the email, and with **Send with Attachment** in Delivery Settings it also attaches the Delivery Note print. It did not check that the user who sends the email can read those Delivery Notes. Now it checks read permission on each Delivery Note in the stops before any email is sent.

**Fix:** In `notify_customers`, check read permission (with user permissions) once for each distinct Delivery Note in the stops, before the emails are made. () The follow-up test commit checks a user who can read the Delivery Note of the first stop but not the one of the second stop. ()

**Changes compared with develop:** None. The commit applies without changes. The develop PR has one commit and no follow-up commits. The open PR #67024 (backport of #65792) also changes `delivery_trip.py` and `test_delivery_trip.py`, in other functions. Each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_dispatch_mail_needs_delivery_note_access`: passes on this branch, fails on `version-16-hotfix` without the fix (no permission error for the Fulfillment User). The same test checks that a Stock User still sends the emails.
- `test_dispatch_mail_needs_access_to_every_delivery_note`: a Stock User with a User Permission for only the Delivery Note of the first stop gets a permission error, and no email is sent. Passes on this branch, fails on `version-16-hotfix` without the fix, and fails when the check is made without the Delivery Note name.
- `test_delivery_trip.py` (complete file): 29 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `94719d70d646`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.