# Issue

**Title:** fix(stock): deliver a bundle component from each warehouse it is picked from (backport #66296)

## Description

**Problem:** When a Pick List picks a Product Bundle component from two warehouses, a Delivery Note or Sales Invoice made from it gets one packed row for the whole qty. That row has the warehouse and serial nos of only one Pick List row, so submit fails on available qty.

**Solution:** Pack the component from each Pick List row that is not delivered yet, one packed row per row, each with its own warehouse, batch and serial nos. A re-save keeps the rows it packed before, including serial nos the user changed. All split rows deliver the same Sales Order packed row, so stock reservations are delivered per warehouse. A repost updates the rate of each split row from its own warehouse or bundle. A return packed row links the delivered packed row it reverses (`return_against_packed_item`). A partial return fills each delivered row up to what is left to return on it, and each row comes back at its delivered rate.

### Steps to reproduce
1. In Stock Settings, enable "Use Serial / Batch Fields".
2. Make a Product Bundle with 1 of a serialized stock item as its component.
3. Receive 2 serial nos of the component into warehouse A and 2 into warehouse B.
4. Submit a Sales Order for 4 bundles. Make a Pick List from it (it picks 2 from A and 2 from B) and submit it.
5. On the Pick List, click Create > Delivery Note and submit it.

Before: one packed row of 4 in one warehouse with 2 serial nos; submit fails "Available qty 2.0 is less than the Required Qty 4.0".
After: two packed rows, 2 from A and 2 from B, each with its serial nos; the Delivery Note submits and the Pick List is fully delivered. A Sales Return of it returns 2 to each warehouse.

Return (FIFO component, 2 received into A at 100 and 2 into B at 200, same steps without serial nos):
6. On the Delivery Note, click Create > Sales Return, set qty -1, save and submit.
7. Make another Sales Return of the rest and submit it.

Before: step 6 gets -0.5 on each packed row and a whole-number UOM refuses it; a full return takes back 200 + 200 after 200 + 400 went out.
After: step 6 takes back -1 from one row and 0 from the other; step 7 takes back the rest, each row at its delivered rate (100 and 200).

<hr>This is an automatic backport of pull request #66296 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8ed342331912`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.