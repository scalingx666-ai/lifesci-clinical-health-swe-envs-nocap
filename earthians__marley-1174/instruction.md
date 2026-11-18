# Issue

**Title:** fix(therapy): practitioner mapping when creating Therapy Session from  Service Request or Therapy Plan

## Description

Issue description:
When a Patient Encounter is submitted for a therapy type, the system creates both a Therapy Plan and a Service Request with the practitioner populated correctly. 

However, when a Therapy Session is later created from either service request or therapy plan , the practitioner is not carried forward because make_therapy_session() only relied on the optional practitioner argument, while the current creation flows do not pass that value.

Fix applied:
Updated make_therapy_session() in therapy_plan.py to resolve practitioner from the source flow when it is not passed explicitly.

Logic change added:
- If the Therapy Session is created from a Service Request, practitioner is fetched from Service Request.practitioner.
- If the Therapy Session is created from a Therapy Plan, practitioner is fetched from Therapy Plan.practitioner.
- If a practitioner is explicitly passed to the method, that value still takes priority.
- Existing department assignment logic remains unchanged and continues to derive department from the resolved practitioner.

Test scenario:
- Create and submit a Patient Encounter with a therapy type and practitioner so that both a Therapy Plan and a Service Request are generated. 
- Then create a Therapy Session from the Service Request and verify the practitioner is fetched from the Service Request. 
- Next, create a Therapy Session from the Therapy Plan and verify the practitioner is fetched from the Therapy Plan, with the practitioner field populated in both flows.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b9dc656dd55`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.