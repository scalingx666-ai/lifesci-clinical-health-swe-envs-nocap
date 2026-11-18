# Issue

**Title:** BFD inpatient exporter updates

## Description

- Ensure claim totals match sum of line items
- Always have a total charge line item
- Improve mapping from procedure code to revenue center

NOTE: uses new inpatient_rev_cntr_code_map.json file that is not checked in

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f838c51c90fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.