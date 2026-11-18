# Issue

**Title:** Fix Go FHIR JSON parser handling of JSON null with newer json-iterator versions.

## Description

Fix Go FHIR JSON parser handling of JSON null with newer json-iterator versions.
json-iterator v1.1.11+ decodes a JSON null into a nil json.RawMessage instead of
the literal "null"; restore the literal after decoding so null fields and null
array elements keep being treated as null.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c0066974970`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.