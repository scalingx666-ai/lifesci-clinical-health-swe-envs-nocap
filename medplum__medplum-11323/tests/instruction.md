# Issue

**Title:** [SchedulingWorkspace] Reveal full visit-type list in dropdown

## Description

The common scenario here is that there is a relatively small set of HealthcareService records, and it can be helpful for the viewer to see that entire list to help them guide their selection.

- We now try to load a first page of 100 results; if that page is not full, then we know we have the "complete" catalog of visit types. In that case we can apply filtering client-side and avoid additional round-trips.

- If the results don't fit into that page, we continue using server-backed search.

- In each case, we now use a "contains" style search (case-insensitive match anywhere in the string) instead of the default "prefix" style matching we used before. This means that typing "imaging" would match "Ultrasound Imaging", for instance.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `14ad9501016d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.