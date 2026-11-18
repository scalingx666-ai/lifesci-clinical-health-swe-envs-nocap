# Issue

**Title:** fix Patient identifiers (SSN, DRIVERS, PASSPORT) are not unique — collisions at population scale

## Description

PASSPORT identifier format losing low-bound offset

SSN/DRIVERS/PASSPORT are not required to be unique per #1685
discussion, so no changes there — this only fixes the format bug.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ffe7bc7f139`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.