# Issue

**Title:** FHIR-54447: When would a MedicationRequest be "based on" another Medica^E

## Description

Resolves [FHIR-54447](https://jira.hl7.org/browse/FHIR-54447): When would a MedicationRequest be "based on" another MedicationRequest vs "replace" it?

## What changed
Added the same comment to MedicationRequest.basedOn and MedicationRequest.priorPrescription in structuredefinition-MedicationRequest.xml, explaining that a request based on an authorization (an instance order based on an order, or an order based on a proposal) uses basedOn, and one that replaces or follows a prior order (continuation or refill) uses priorPrescription; the wording is lightly edited from the resolution text. Recorded the change under "Changes since 6.0.0-ballot5" in medicationrequest-introduction.xml. The build updated medicationrequest-request-mapping-exceptions.xml with the new comment text.

## Files touched
- `source/medicationrequest/medicationrequest-introduction.xml`
- `source/medicationrequest/medicationrequest-request-mapping-exceptions.xml`
- `source/medicationrequest/structuredefinition-MedicationRequest.xml`

## Publisher QA

- errors: 0
- warnings: 88
- info: 1
- broken_links: 0

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d38fdc25df1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.