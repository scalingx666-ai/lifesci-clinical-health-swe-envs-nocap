# Issue

**Title:** FHIR-58457: MedicationRequest.statusChanged is when the status was last changed

## Description

Resolves [FHIR-58457](https://jira.hl7.org/browse/FHIR-58457): Clarify that statusChanged represents the date/time of the most recent status change.

## What changed
- `MedicationRequest.statusChanged`
  - definition: "The date (and perhaps time) when the status was changed." → "The date (and perhaps time) when the status of the MedicationRequest was last changed." (as requested)
  - short: "When the status was changed" → "When the status was last changed"
- Release note under "Changes since 6.0.0-ballot5" in the MedicationRequest introduction.

## Build
Summary Errors=0. Checked: the definition and short on medicationrequest-definitions.html; the release note on medicationrequest.html.

Note: #4347 and #4354 also add entries to the MedicationRequest release-note list – a small merge for whichever is merged later.

Disposition: Persuasive

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `064ca22f9527`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.