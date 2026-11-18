# Issue

**Title:** Flexporter enhancements

## Description

This PR adds a few enhancements identified when trying to create "Not Done" type resources for QICore. (Ex, Medication Not Requested https://build.fhir.org/ig/HL7/fhir-qi-core/StructureDefinition-qicore-medicationnotrequested.html )

- Disables the annoying warning the flexporter introduced. For a single patient it wasn't that big a deal but for larger populations it made it impossible to follow the output.
- Adds a "fullUrl" field to the Bundle entry on any created resources
- When creating resources based on a given state, adds the ability to reference the Encounter that was active at that time
- Adds a specific "No Aspirin" state to the ACS Discharge Meds submodule for the flexporter to key off of for this example. We may want to make it a "best practice" to have an actual empty simple-type state in modules when a treatment option is skipped, to make it easier to identify.
- Adds a flexporter mapping in src/test/resources with a new Not Done example. Try running it with `./run_synthea -fm src/test/resources/flexporter/qicore_withnotdone.yaml -k must_have_cardiac_surgery.json -a 55-65`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `85673dfd1503`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.