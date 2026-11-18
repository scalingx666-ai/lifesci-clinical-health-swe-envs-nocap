# Issue

**Title:** Flexporter - Update randomCode fn to take output type as an optional second param

## Description

Updates to address flexporter issues identified by @elsaperelli :

1. I realized the `randomCode` function was improperly named since technically it produces a Coding not a code. Rather than rename it and break backwards compatibility, this gives it an optional second parameter for "return type". This can be "code" to return a string, "Coding" to return a Coding (ie `{system, code, display}`), or "CodeableConcept" to return a CodeableConcept. Default if unspecified is Coding, for backwards compatibility.

2. Adds support for defining custom ValueSets in a flexporter mapping file, so that you can select a randomCode from your handpicked set of codes rather than having to use a terminology server and pre-existing VS. The syntax is a YAML version of the ValueSet resource, to minimize inventing new things. There are some quirks to this though so I'm open to suggestions here:
    - Our YAML parser doesn't work with the HAPI FHIR model classes, so this uses a roundabout way of loading that parses the YAML to `Map<String,Object>`, serializes that to JSON, then parses the JSON as FHIR. The alternative here would be to define a custom new model to represent a VS, or to re-implement the ValueSet class.
    - The ValueSets need to be loaded once per mapping file, so I added a new function to be called in the main flexporter entrypoints (App and RunFlexporter). Trying to load them multiple times wouldn't break anything but I don't want to do that (YAML) -> (JSON) -> (FHIR classes) sequence multiple times unnecessarily.

3. Added some extra error handling for the value set $expand operation, to assist in debugging when it returns an OperationOutcome

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2cc0a62b07e8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.