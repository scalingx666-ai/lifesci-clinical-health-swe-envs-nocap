# Issue

**Title:** FHIR-56335: MedicationRequest.intent - use the Request intent code system

## Description

## Summary

[FHIR-56335](https://jira.hl7.org/browse/FHIR-56335) – MedicationRequest.intent - use Request CodeSystem (Persuasive with Modification):
> Remove the medication specific codesystem and use the codesystem from the pattern, making sure that the ValueSet includes only the current existing codes - i.e not adding any codes, just switching code systems

## Changes

- `valueset-medicationrequest-intent.xml`: includes `http://hl7.org/fhir/request-intent` with the 8 current codes listed explicitly (proposal, plan, order, original-order, reflex-order, filler-order, instance-order, option). `directive`, `solicit-offer`, `offer-response` (and `other`) from the Request code system are not included.
- `codesystem-medicationrequest-intent.xml`: removed.
- Value set URL and OID, and the `MedicationRequest.intent` binding (required), are unchanged. `oids.ini` keeps the code system's OID line, as for earlier removals.
- Release note under "Changes since 6.0.0-ballot5" in `medicationrequest-introduction.xml`.

## QA

- Local build: `Summary: Errors=0` (partial build). No MedicationRequest warnings; the warnings in the log are in unrelated resources.
- Generated `valueset-medicationrequest-intent.html`: "Include these codes as defined in http://hl7.org/fhir/request-intent"; the expansion has 8 concepts.
- Release note shown on `medicationrequest.html`.

## Related

- [FHIR-55336](https://jira.hl7.org/browse/FHIR-55336) (add "other", deprecate the medication code system) is not included. Its "deprecate" step is superseded by this removal. "other" is not yet in the built Request intent code system: FHIR-56142 added it to `source/request/codesystem-request-intent.xml`, but the build uses the `request-intent` worksheet in `request-spreadsheet.xml`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5bf9174bbd97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.