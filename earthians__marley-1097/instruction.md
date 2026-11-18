# Issue

**Title:** fix: add inpatient_record in diagnostic report (backport #1089)

## Description

Issue:
Diagnostic Report did not have an inpatient_record field, which made it difficult to distinguish inpatient and outpatient diagnostic reports. This impacted both laboratory and imaging-related report handling where OP/IP context is needed.

This change adds a readonly inpatient_record field to Diagnostic Report and fetches its value from the linked Patient record using fetch_from: "patient.inpatient_record".

With this update:
Diagnostic Reports can carry the patient’s inpatient reference directly
OP and IP reports can be differentiated more easily
The change stays minimal and limited to the DocType JSON definition only

Fix applied:
Added inpatient_record to the Diagnostic Report field list and field order in diagnostic_report.json

Test Cases:-
Create Encounter for both laboratory and imaging observation templates and check whether the generated report has inpatient record.
no-docs<hr>This is an automatic backport of pull request #1089 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63411b6d6681`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.