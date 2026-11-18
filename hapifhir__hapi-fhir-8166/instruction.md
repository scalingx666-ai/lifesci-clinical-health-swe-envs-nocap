# Issue

**Title:** Update to org.hl7.fhir.core 6.9.12

## Description

This updates org.hl7.fhir.core to 6.9.12

Notes regarding these changes:

okhttp_version was updated to 5.3.2 for two reasons:
 - org.hl7.fhir.core uses that same version, and this prevents us from having to track two different versions in our code.
 - the okio library in the older versions of okhttp contained vulnerabilities (this is why org.hl7.fhir.core updated its version of the library)
 
There was a pinned okio dependency in dependencyManagement that is no longer needed, as the okio dependency used by the more current okhttp is more recent, and has no known vulnerabilities. 

kotlin.version was also updated in hapi-fhir-base-test-jaxrsserver-kotlin as this was old and incompatible with the kotlin used in the new okio

There are a number of added methods, altered signatures, and updated tests that correspond to the ones done in HAPI master in the following PRs:

 <- simple dependency update
 <- slightly more complex dependency updates to allow for org.hl7.fhir.core's usage of spotugs, which impacted JavaDoc generation
 <- changes to pom.xml and to numerous classes to account for changed method signatures in org.hl7.fhir.core. All of the functional changes are very minimal, applying to methods that have always returned null, or have had no-op functionality. There is one change to validation output, which was accepted by reviewers in this pull as correct.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e21b151a01fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.