# Issue

**Title:** fix(subcontracting): replay each remaining transfer on the reservations made before it

## Description

Depends-On: #67173

**Problem:** when a Send to Subcontractor entry transferred more than the order's open reservation, and the order reserved more stock later, cancelling the later transfer does not reopen the later reservation. develop takes the cancelled qty off the oldest reservation (Transferred Qty 4 and 2). #67173 rebuilds from the pooled qty of the remaining transfers, so the unreserved part of the first transfer lands on the later reservation (6 and 2), and the 2 units the order still needs are no longer reserved.

**Fix:** the rebuild replays each remaining transfer, oldest first, only on the reservations made before it, the same way submit spread it. A transfer is timed by its first stock ledger entry (kept when its ledger is recreated), so a draft made before a reservation but submitted after it is still placed as on submit.

This does not store the split at submit; it re-derives it. It gives the submit-time split as long as the reservations a transfer saw are still the ones before it (a reservation cancelled since is left out either way).

### Steps to reproduce
1. In Stock Settings, turn on "Enable Stock Reservation" and "Allow Partial Reservation".
2. Raw material RM, subcontracted item whose BOM uses 1 RM. Receive 6 RM into Stores.
3. Submit a Subcontracting Order for 10 with Reserve Stock on (reserves 6).
4. Receive 2 more RM into Stores, then Send to Subcontractor 8 RM.
5. Receive 2 more RM into Stores, Reserve 2 on the order, then Send to Subcontractor 2 RM.
6. Cancel the entry from step 5.

Before: the Stores reservations show Transferred Qty 6 and 2, both closed. After: 6 and 0, and the order holds 2 RM reserved again.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c8576d9754e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.