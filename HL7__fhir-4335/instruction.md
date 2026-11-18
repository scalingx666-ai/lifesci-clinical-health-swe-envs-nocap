# Issue

**Title:** FHIR-55331: Spelling/abbreviation issues on page: dosage-examples

## Description

Resolves [FHIR-55331](https://jira.hl7.org/browse/FHIR-55331): Spelling/abbreviation issues on page: dosage-examples

## What changed
Spelled out the five contractions on the dosage examples page (dosage-examples.html): "it’s", "don’t", "There's", "shouldn’t" and "There’s" become "it is", "do not", "There is", "should not" and "There is". The possessive "FHIR's" in a CSS comment is not a contraction and was left unchanged.

## Files touched
- `source/dosage-examples.html`

## Publisher QA

- errors: 0
- warnings: 17
- info: 1
- broken_links: 0

**Deviation from the resolution (requested in review):** in the first note under Example 4, "/m2" is written as "/m²", "skin surface area" is changed to "body surface area (BSA)", and a full stop is added.

Note: PR #4327 (FHIR-54341) also edits dosage-examples.html (Example 4 startOffset), on different lines.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d38fdc25df1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.