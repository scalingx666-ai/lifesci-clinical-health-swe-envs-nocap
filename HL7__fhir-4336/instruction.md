# Issue

**Title:** FHIR-54523: Example 1 structure view dose 10 mg -> 2.5 mg

## Description

## Summary

[FHIR-54523](https://jira.hl7.org/browse/FHIR-54523) – Dosage examples: text vs structure mismatches (Persuasive with Modification).

PR #4008 applied the resolution: Example 1's doseQuantity changed from 10 mg to 2.5 mg in the JSON and XML. The YAML structure view of the same example still showed `doseQuantity: 10 mg`, so the example still disagreed with itself; this was found when checking the ticket against build.fhir.org.

This PR changes that one line in `source/dosage-examples.html` to `doseQuantity: 2.5 mg`.

## QA

- Local build: `Summary: Errors=0, Warnings=0, Information messages=0`.
- Generated `publish/dosage-examples.html`: Example 1 structure view shows `doseQuantity: 2.5 mg`. The other 10 mg values belong to Example 2 and later, where they are correct.
- No release note: dosage-examples.html is not a resource page (same as #4327 and #4335).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d38fdc25df1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.