# Issue

**Title:** fix: use yhat for zdiff and z-score for zgain

## Description

we also fix one more small bug when loading results (we drop the subs_id early to make sure the loaded matrix of 'z', 'yhat' etc) is a float64 and not an object (with both text and numbers)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe9631d511ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.