# Issue

**Title:** RIF Hospice Consolidation

## Description

- Break up RIF `HospiceExporter.export` function to make the flow clearer
- Break up RIF `SNFExporter.export` function to make the flow clearer
- Add claim line consolidation to Hospice export to reduce the number of claim lines per claim
- Fix deprecation warning re `new Double(0.0)`
- Fix gradle deprecation warning re dependency version fixing

Note: requires new hospice_rev_cntr_code_map.json file available from the usual places.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f3ad98666a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.