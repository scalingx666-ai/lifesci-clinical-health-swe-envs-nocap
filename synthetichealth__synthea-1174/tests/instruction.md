# Issue

**Title:** BFD RIF total charge claim line

## Description

- Update BFD HHA exporter to add total charge revenue center line to all claims
- Update BFD SNF exporter to add total charge revenue center line to all claims
- Consolidate HHA claim periods by provider
- Separate consolidated claim lines by clinician
- Fix bug in claim cost aggregation for medications
- Rename some claim methods for clarity
- Fix bug in SNF.REV_CNTR_RATE_AMT calculation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2fd1e9642436`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.