# Issue

**Title:** fix(stock): check POS Invoice read and warehouse access in get_pos_reserved_serial_nos (backport #66003)

## Description

Backport of #66003 to `version-15-hotfix`. The version-16 backport is #67095.

`get_pos_reserved_serial_nos` gives the Point of Sale the serial numbers that submitted POS Invoices hold for an item in a warehouse. It did not check any permission. It now needs read permission on POS Invoice and access to the warehouse.

**Fix:** `get_pos_reserved_serial_nos` checks read permission on POS Invoice and select permission on the warehouse. ()

**Test (follow-up):** the test submits a POS Invoice for a serial number, so the permitted user must get that serial number back. ()

**Changes compared with develop:** The function on this branch reads the POS Invoice rows itself, and has no Item select check (that check comes from an earlier develop change that is not on this branch; this PR does not add it). The two checks are added at the start of the function. The develop test is in `erpnext/stock/tests/test_serial_batch_identity.py`, which does not exist on this branch. The test is ported to `test_serial_no.py` with `create_user` and `add_user_permission`. The develop test patches `get_reserved_serial_nos_for_pos`, which does not exist here, so the ported test submits a real POS Invoice for a serial number (with an open POS Opening Entry) and checks that the permitted user gets that serial number. The permission assertions are the same. Other PRs to `version-15-hotfix` that change `serial_no.py` and `test_serial_no.py`: #67094. Both PRs add the same `from erpnext import require_permission` import; the other changes are on different lines, and each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_pos_screen_reservation_lookup_requires_pos_invoice_and_warehouse_permission`: passes on this branch (the permitted user gets the reserved serial number), fails on `version-15-hotfix` without the fix.
- `test_serial_no.py` (complete file): 10 tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.