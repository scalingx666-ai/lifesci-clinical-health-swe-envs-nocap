# Issue

**Title:** Fix BP code to be the required code.

## Description

BP code was incorrect in 1 out of 9 instances in the modules where BP was recorded.

See

- Stackoverflow  thread https://stackoverflow.com/questions/71246204/fhir-to-omop-mapping-question-blood-pressure-systolic-and-diastolic-with-unmapp/71246501#71246501
- FHIR Spec http://hl7.org/fhir/STU3/observation-vitalsigns.html

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d388c9943b03`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.