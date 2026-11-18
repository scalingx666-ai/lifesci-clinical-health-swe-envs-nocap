# Issue

**Title:** [Scheduling] Exclude inactive service facilities

## Description

If a service facility is inactive (`Location.status`), then that should signal that it is not currently accepting appointments under it. Previously we had no status filter on service facilities anywhere in our scheduling workspace. 

As some organizations may want to go live incrementally by service facility, we need a mechanism to be able to define which SFs are "live" and which are not. `Location.active` is the most intuitive place for this to live, both inherently with its element meaning, and since other scheduling workspace functionality filters out inactive resources from being selected in the workflow.

An inactive service facility will _not_ prevent resources associated with that service facility from being included in an appointment, so long as the appointment itself is not associated with that service facility (including if it's unset).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2a9ac9b05c1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.