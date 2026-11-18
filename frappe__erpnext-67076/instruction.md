# Issue

**Title:** fix(subcontracting): check Subcontracting Inward Order read permission in get_fg_reference_names (backport #65794)

## Description

Backport of #65794 to `version-16-hotfix`.

`get_fg_reference_names` (the search behind the **Against Finished Good** field in a "Receive from Customer" Stock Entry) returned the finished good rows of any submitted Subcontracting Inward Order named in the filter, without checking that the user can read that order. It now checks read permission on the Subcontracting Inward Order, and returns nothing when the order filter is not a plain name.

**Fix:** `get_fg_reference_names` checks read permission on the Subcontracting Inward Order before it reads its rows, and returns an empty list when the order filter is empty or not a string. ()

**Changes compared with develop:** The signature of `get_fg_reference_names` conflicted, because develop has type annotations on it. The signature of this branch is kept, and the new check is added to its body.

 for the example and the steps to test.

### Tests

- `test_fg_reference_names_follow_inward_order_read_access`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_subcontracting_inward_order.py` (complete file): 11 pass. The other 50 tests fail the same way on `version-16-hotfix` without this change on the local test site (`NamingSeries.get_current_value()` TypeError, and a missing Subcontracting BOM test record that follows from it).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.