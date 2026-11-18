# Issue

**Title:** fix(discharge-summary): discharge summary naming series when created from inpatient record

## Description

Issue Description:-
  When a Discharge Summary is created from an Inpatient Record using the mapped document flow, it inherits the Inpatient
  Record naming_series. This causes the Discharge Summary to use the inpatient prefix, such as HLC-INP-.YYYY.-, instead
  of its own configured series HLC-DS-.YYYY.-.

  Manually created Discharge Summary records work correctly because they use the doctype default series.

  Fix Applied
  Updated the Inpatient Record to Discharge Summary mapper to exclude naming_series from copied fields. This allows the
  Discharge Summary doctype default naming series to be applied during creation.

Before:
<img width="733" height="266" alt="image" src="https://github.com/user-attachments/assets/0d87fe05-06f3-43e8-a6ae-d12160e9ce38" />

After fix:
<img width="665" height="280" alt="image" src="https://github.com/user-attachments/assets/ae4bcfb1-6c87-40c2-b325-43f228925866" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e67142cbc2a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.