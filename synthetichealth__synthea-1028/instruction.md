# Issue

**Title:** Metabolic syndrome module refactor

## Description

This PR refactors and simplifies the metabolic syndrome modules, currently `metabolic_syndrome_disease` and `metabolic_syndrome_care`, by breaking out major pieces into submodules and other top-level modules:

 - `metabolic_syndrome_disease`
   - extracted CKD into a separate module
   - refactored onset - previously diabetes onset would happen with a uniform distribution between 18, now the onset range has been adjust to more accurately reflect onset rates
   - extracted HTN onset into the hypertension module, previously it would only happen at age 18 or at onset of diabetes, now it has a race-and-sex specific rate per year
 - `metabolic_syndrome_care`
   - extracted submodules:
   - medications
   - care for eye conditions
   - care for kidney conditions
   - amputations 
 - `chronic_kidney_disease`
 - `hypertension`
 - `wellness_encounters`
   - obesity check moved here

Note: this was originally done on the `cabg_cardio_gmf_htn_trial` branch, but sending this separately in an attempt to clean up and harmonize our branches.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63421913bbba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.