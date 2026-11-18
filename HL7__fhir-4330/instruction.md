# Issue

**Title:** FHIR-54375: isActive and role have duplicate definitions

## Description

Resolves [FHIR-54375](https://jira.hl7.org/browse/FHIR-54375): isActive and role have duplicate definitions

## What changed
Replaced the definition of Medication.ingredient.role in structuredefinition-Medication.xml, which duplicated the isActive definition, with "The (typically coded) functional role of the ingredient - for example active, excipient, adjuvant, solvent etc.", and recorded the change under "Changes since 6.0.0-ballot5" in medication-introduction.xml. The resolution also says to keep the comment about role complementing isActive; role has no comment in the current source, so nothing else changed.

## Files touched
- `source/medication/medication-introduction.xml`
- `source/medication/structuredefinition-Medication.xml`

## Publisher QA

- errors: 0
- warnings: 38
- info: 3
- broken_links: 0

Note: PR #4329 (FHIR-54379) adds a line to the same "Changes since 6.0.0-ballot5" list in medication-introduction.xml; whichever merges second may need a one-line rebase.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d38fdc25df1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.