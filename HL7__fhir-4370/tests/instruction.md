# Issue

**Title:** FHIR-58907, FHIR-58386: renderedInstruction definition and comment (optional)

## Description

Resolves [FHIR-58907](https://jira.hl7.org/browse/FHIR-58907) (renderedInstruction should be optional – Persuasive with Modification) and [FHIR-58386](https://jira.hl7.org/browse/FHIR-58386) (renderedInstruction 1..1 should be 0..1 – Persuasive, same change), voted 2026-10-19.

**Based on #4347** (FHIR-54340, DosageDetails renamed DosageInstruction): this PR targets that branch, so the diff shows only this change. Once #4347 is merged, it is retargeted to master.

## What changed
`DosageInstruction.renderedInstruction` stays 0..1 (reverting the effect of FHIR-54014; it was changed back to 0..1 on 2026-09-08), and the requirement wording is removed:
- Definition: "The full representation of the dosage instructions, as text for display to and use by humans."
- Comment: "`renderedInstruction` SHOULD be present when the dosage is intended to be read and acted on by people, such as prescribers, pharmacists, those administering the medication, or the patient. It can be omitted when the exchange does not need a human-readable rendering of the dosage, such as for logistics or supply where the dosage is not acted upon. When present, it SHALL be consistent with the structured dosage, and may contain additional information not found in the structured content. See [Dosage text and structured data](dosage.html#text)."
- Release note under "Changes since 6.0.0-ballot5" on the Dosage page.

## Build
Summary Errors=0; the element is 0..1 with the new definition and comment; the release note is on dosage.html.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a1b865a6006`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.