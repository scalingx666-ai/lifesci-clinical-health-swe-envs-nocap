# Issue

**Title:** QA: Update the r5-r6 mappings for Goal and ClinicalUseDefinition (take2)

## Description

## Description

QA: Update the R5 to R6 mappings for the diff tab _(after checking with editors/owners)_:
* Goal https://chat.fhir.org/#narrow/channel/294552-Patient-Care-WG/topic/Goal.20R5.20to.20R6.20mapping/with/607968126
* ClinicalUseDefinition [#committers > ClinicalUseDefinition](https://chat.fhir.org/#narrow/channel/179165-committers/topic/ClinicalUseDefinition/with/607964829)

(same as #4272 - just in a new branch to test the build issue)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a184fb8bad39`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.