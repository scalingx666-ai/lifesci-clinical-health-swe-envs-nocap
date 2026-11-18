# Issue

**Title:** fix: validate patient on nursing care plan admission

## Description

Issue description: 

When manually creating a Nursing Care Plan, a user can select one patient and an Inpatient Record belonging to another patient. The form saves because it checks the admission’s status but does not verify that the admission belongs to the selected patient.

Fix applied / changes made: 
1. Added save-time validation that rejects an inpatient record when its patient differs from the care plan’s patient. Added a regression test for this mismatch. 

2. Existing care plans linked to another patient’s admission could block discharge after this new validation was added. During discharge, clear the incorrect admission link before closing the plan. Added a regression test for this case

After fix:
<img width="597" height="178" alt="image" src="https://github.com/user-attachments/assets/51ce57c7-a562-4a3f-9301-48ba2681756e" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `357eca830944`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.