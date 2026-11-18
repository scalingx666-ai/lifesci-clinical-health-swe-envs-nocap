# Issue

**Title:** FHIR-54341: StartOffset in example 8

## Description

Resolves [FHIR-54341](https://jira.hl7.org/browse/FHIR-54341): StartOffset in example 8

## What changed
Changed the startOffset of the Day-8 component in Dosage Example 4 (dosage-examples.html) from 8 to 7 days in the bullet text, YAML, JSON and XML, so that the dose falls on Day 8 of each 28-day cycle; the ticket was raised against Example 8 but the resolution applies it to Example 4.

## Files touched
- `source/dosage-examples.html`

## Publisher QA

- errors: 0
- warnings: 114
- info: 1
- broken_links: 0

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d38fdc25df1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.