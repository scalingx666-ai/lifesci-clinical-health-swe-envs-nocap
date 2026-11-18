# Issue

**Title:** fix(subcontracting): don't cancel a used Subcontracting Order reservation

## Description

**Problem:** a Subcontracting Order reservation that a Subcontracting Receipt consumed can be cancelled, by Unreserve or by closing the order. Its consumed qty then stays only on the cancelled reservation, so cancelling that receipt later reopens a newer reservation that a later receipt still consumes. `before_cancel` blocks used reservations only for Work Orders, and closing the order keeps only reservations with transferred qty.

**Fix:** treat a Subcontracting Order like a Work Order: a reservation with transferred or consumed qty cannot be cancelled while the order is open (close the order to release the unused stock), and closing keeps the used qty of a consumed reservation reserved, as it already does for transferred qty.

Unreserve on a reservation with only transferred qty is now refused too, as for Work Orders. #67174 changes how a receipt cancel reopens reservations; this PR only stops the reservation from being cancelled in the first place.

### Steps to reproduce
1. In Stock Settings, turn on "Enable Stock Reservation" and "Auto Reserve Serial and Batch".
2. Batched raw material, subcontracted item whose BOM uses 1 of it. Receive 10 of the raw material.
3. Submit a Subcontracting Order for 10 with Reserve Stock on.
4. Send to Subcontractor 6, then a Subcontracting Receipt for 6.
5. On the order, Unreserve the supplier warehouse reservation (Consumed Qty 6).
6. Send to Subcontractor 4, then a Subcontracting Receipt for 4.
7. Cancel the first receipt.

Before: step 5 cancels the reservation, and after step 7 the new reservation shows Consumed Qty 0 while the second receipt still consumes 4. After: step 5 fails with "already used by Subcontracting Order ... Close the Subcontracting Order to release the unused stock".

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa728f6a54bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.