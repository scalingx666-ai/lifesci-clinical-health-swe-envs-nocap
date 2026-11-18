# Issue

**Title:** RDF R6 updates FHIR-57496 & FHIR-55250

## Description

# https://jira.hl7.org/browse/FHIR-57496
This PR updates guidance on using RDF concept IRIs. Previously it was recommended to add concept IRIs using a `rdf:type` assertion on FHIR Coding. This was inappropriate for most concepts (e.g. a FHIR Coding is not an instance of SNOMED "Body Weight"). 
Now, the recommendation is to use either `rdf:type` assertion on CodeableConcept where appropriate (as in [DSTU2](https://hl7.org/fhir/DSTU2/rdf.html#1.18.3.4.5)), or a more neutral , or both.

# https://jira.hl7.org/browse/FHIR-55250 & conformance language
This PR also fixes more typos, adds missing `<code>` tags for RDF terms, fixes improperly formatted RDF code blocks, and aligns more of the conformance language used to what is expected (see https://ginoc.io/fmg-review/#/wg/its/page/409 and https://build.fhir.org/conformance-rules.html#conflang).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f5f45d07e17e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.