# Issue

**Title:** (fix) remove imports from querystring in three components (ledger-cre…

## Description

There were imports from querystring in three components which was breaking the angular build,
* ledger-create-shared.component.ts
* billing-receipt-old.component.ts
* ssu-patient.component.ts

That was unused imports, hence removing imports from querystring solved the issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fbed36e571ac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.