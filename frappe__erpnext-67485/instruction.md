# Issue

**Title:** fix(subcontracting): keep Subcontracting Delivery button while overproduced goods are left

## Description

**Problem:** with Allow delivery of overproduced quantity on, the server lets the user deliver all produced finished goods, but the Create > Subcontracting Delivery button went away at % Delivered 100.

**Fix:** also show the button while a finished good row has more produced than delivered and the setting is on. The setting is sent to the form in its onload.

Checked by reading the code; no browser run.

### Steps to reproduce
1. Manufacturing Settings: Overproduction Percentage For Work Order 20. Selling Settings: Allow delivery of overproduced quantity on.
2. Make an inward order for 5 FG and submit a Manufacture entry for 6.
3. Deliver 5 with Create > Subcontracting Delivery.

Before: the Create menu has no Subcontracting Delivery for the sixth unit. After: it is there.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4f675270770`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.