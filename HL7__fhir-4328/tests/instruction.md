# Issue

**Title:** FHIR-54372: Consider Status-timestamp invariants

## Description

Resolves [FHIR-54372](https://jira.hl7.org/browse/FHIR-54372): Consider Status-timestamp invariants

## What changed
Lowered the severity of invariant mdd-1 (whenHandedOver cannot be before whenPrepared) on MedicationDispense from error to warning in structuredefinition-MedicationDispense.xml, leaving its expression unchanged, and recorded the change under a new "Changes since 6.0.0-ballot5" note in medicationdispense-introduction.xml. No new status/timestamp invariants were added, as the resolution (Not Persuasive with Modification) declines them.

## Files touched
- `source/medicationdispense/medicationdispense-introduction.xml`
- `source/medicationdispense/structuredefinition-MedicationDispense.xml`

## Publisher QA

- errors: 0
- warnings: 179
- info: 3
- broken_links: 0

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5bf9174bbd97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.