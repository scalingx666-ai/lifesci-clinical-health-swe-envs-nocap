# Issue

**Title:** WAIT: New RIF fields

## Description

Add new RIF field codes:

- Add CLAIM_QUERY_CODE to HHA and Hospice
- Add CARR_CLM_BLG_NPI_NUM to Carrier
- Add COVSTART, PTA_CVRG_STRT_DT, PTA_CVRG_END_DT, PTB_CVRG_STRT_DT, PTB_CVRG_END_DT, PTD_CVRG_STRT_DT, PTD_CVRG_END_DT to Beneficiary

, .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f26777c403bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.