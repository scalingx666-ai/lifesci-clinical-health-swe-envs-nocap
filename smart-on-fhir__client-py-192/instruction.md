# Issue

**Title:** server: send correct Accept=application/fhir+json HTTP headers

## Description

First and foremost, stop requesting application/json for FHIR objects. The correct type is application/fhir+json. The [spec](https://www.hl7.org/fhir/R4/http.html) says:

"The correct mime type SHALL be used by clients and servers: JSON: application/fhir+json"
and
"If a client provides a generic mime type in the Accept header (application/xml, text/json, or application/json), the server SHOULD respond with the requested mime type, using the XML or JSON formats described in this specification as the best representation for the named mime type (except for binary - see the note on the Binary resource)."

So this was only ever working by accident, and wasn't correct for Binary resources, which when provided a non-fhir+json Accept header are supposed to return their binary content, not the FHIR object.

So now we send the right header.

Also for DELETE requests, send signed headers if possible.

Fixes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9556bd33d6da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.