# Issue

**Title:** Claims CSV contains invalid uuids

## Description

Hi,
claims, exported as CSV, contains both, according to the wiki, a Primary Patient Insurance ID and a Secondary Patient Insurance ID of type UUID. However, the code produces 0, if no Payer exists. 0 is not a valid UUID and hence we are unable to import the exported CSV files into a PostgreSQL database.
In case of no Payer exists, I suggest to generate nothing (NULL in SQL speak) instead of 0.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7fcbc66af86d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.