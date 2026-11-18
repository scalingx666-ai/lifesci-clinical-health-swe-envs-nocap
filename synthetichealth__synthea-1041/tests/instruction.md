# Issue

**Title:** Cholesterol model for individuals without diabetes

## Description

One of a few PRs I'll be issuing with features broken out from the `cabg_cardio_gmf_htn_trial` branch, this updates the cholesterol model for individuals without diabetes.  The goal is a more realistic distribution of cholesterol numbers, based primarily on this report: https://www.cdc.gov/nchs/data/databriefs/db363-h.pdf

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5c67e046ac9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.