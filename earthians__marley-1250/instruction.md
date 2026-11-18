# Issue

**Title:** fix: map practitioner on observations and sample collection from service requests

## Description

Issue description:

Observations created from a Service Request were missing the practitioner because the Service Request practitioner was not mapped to Observation.healthcare_practitioner.

For sample collection flows, Sample Collection.referring_practitioner alone was not enough. When a Service Request reused an existing Sample Collection, practitioner attribution could be missing, and when multiple Service Requests shared the same Sample Collection, Observations could be attributed to the wrong practitioner.

Nested sample collection leaves could also lose practitioner attribution because the nested component JSON may not carry the practitioner, causing the Observation to fall back to the collection-level practitioner.

Fix applied:

Mapped Service Request.practitioner to Observation.healthcare_practitioner for direct Observation creation.

Stored practitioner on each Observation Sample Collection row created from a Service Request.

Updated Sample Collection observation creation to prefer the row-level practitioner, then the selected top child row practitioner for nested leaves, and finally Sample Collection.referring_practitioner for existing/manual records.

Passed practitioner into component and non-sample Observation creation helpers so grouped Observation children also receive the practitioner.

Added focused tests to verify practitioner mapping when creating Observations directly from Service Requests and when collecting nested Sample Collection observations using the child row practitioner.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fefe8942cc2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.