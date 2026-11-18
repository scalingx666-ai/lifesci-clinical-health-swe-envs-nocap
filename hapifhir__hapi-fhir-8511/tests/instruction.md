# Issue

**Title:** Fix CDS Hooks deserializer test and run 4 skipped modules in CI

## Description

`CdsServiceRequestJsonDeserializerTest.deserialize_shouldThrow_whenCdsServiceRequestIncludesInvalidProperty` has failed on master since the Jackson 3 upgrade (#8130).

CI didn't catch the failure because `hapi-fhir-server-cds-hooks` is in `.github/config/ignored-modules.yml`. The purpose is to skip demo modules and modules with no tests. Four modules on it are neither, so this PR removes them:

- `hapi-fhir-server-cds-hooks`
- `hapi-fhir-structures-r4b`
- `hapi-fhir-jpa`
- `hapi-fhir-storage-batch2-test-utilities`

**Why the test fails:**
In Jackson 2, unknown properties were rejected with an `InvalidRequestException`. This is no longer the case with Jackson 3. Now, the test asserts that:
- requests with unknown properties succeed but drop unknown properies
- and requests with invalid values are rejected with `InvalidRequestException`

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `215aa0cba6f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.