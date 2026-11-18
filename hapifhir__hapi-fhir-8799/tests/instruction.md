# Issue

**Title:** Exclude the unused FHIR core model and support jars

## Description

Every HAPI consumer ships `ca.uhn.hapi.fhir:org.hl7.fhir.model` (9.6 MB) and the empty `org.hl7.fhir.support`, which arrive through `org.hl7.fhir.convertors` and `org.hl7.fhir.validation`. No HAPI class uses either.

**For review**
- The exclusions sit on the managed `convertors` and `validation` entries in the root pom. `hapi-fhir-converter` and `hapi-fhir-validation` repeat them, because their declarations have exclusions of their own and Maven won't merge managed ones in (rule 6 of `README-hapi-fhir-dependency-versioning.md`, as in #8762).
- `hapi-fhir-converter` lists `org.hl7.fhir.model` as a javadoc `additionalDependency`: its javadoc compiles the convertors sources, which import it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8eafcdb9ad1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.