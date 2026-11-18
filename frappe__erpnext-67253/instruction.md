# Issue

**Title:** fix(subcontracting): return the raw materials a receipt consumed in proportion to the returned qty (backport #66545)

## Description

A Subcontract Return built its supplied items from the BOM (qty per unit × returned qty). When the receipt consumed more raw material than the BOM needs, the return took back less than the receipt consumed for that qty. The finished good row's rate was worked out from that smaller cost, but the stock ledger issued the finished good at its receipt rate, so the difference went to Stock Adjustment. Raw materials the receipt consumed but the BOM does not list were not taken back at all.

Fix: a return takes back the raw materials the returned receipt consumed, in proportion to the finished good qty it sends back. The qty is rounded on the running total of all returns (whole units for serial nos and whole-number UOMs), so together they give back what the receipt consumed; submit stops a return that would take back more. Returns skip the consumed-qty-as-per-BOM check.

### Steps to reproduce
1. In Buying Settings, set "Backflush Raw Materials of Subcontract Based On" to "Material Transferred for Subcontract".
2. In `_Test Company with perpetual inventory`, make a BOM for a subcontracted finished good with one raw material in Kg (qty 1, rate 100).
3. Make a Subcontracting Order for 2 units (service rate 100) and transfer 3 of the raw material.
4. Make and submit the Subcontracting Receipt. It consumes 3 raw material and the finished good rate is 250.
5. Click Create > Subcontract Return, set the finished good qty to -1, save and submit.

Expected: the return takes back 1.5 raw material, the finished good leaves at 250, and nothing is booked to Stock Adjustment. Before this fix it took back 1, showed a rate of 200 and booked 50 to Stock Adjustment - TCP1.

<hr>This is an automatic backport of pull request #66545 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `89f13f3695b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.