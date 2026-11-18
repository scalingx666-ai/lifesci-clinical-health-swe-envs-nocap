# Issue

**Title:** OBLS-901 Added new field negativeInventoryAllowed to the requisition

## Description

Marking orders (requisitions) that allow negative inventory - mainly for PICKUP orders. This field should be set on the integration side

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7f968914fe00`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.