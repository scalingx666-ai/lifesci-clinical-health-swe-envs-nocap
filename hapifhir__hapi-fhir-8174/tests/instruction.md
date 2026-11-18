# Issue

**Title:** Update org.hl7.fhir.core to 6.9.12

## Description

This updates org.hl7.fhir.core to 6.9.12

Notes regarding these changes:

okhttp_version was updated to 5.3.2 for two reasons:

org.hl7.fhir.core uses that same version, and this prevents us from having to track two different versions in our code.
the okio library in the older versions of okhttp contained vulnerabilities (this is why org.hl7.fhir.core updated its version of the library)

There was a pinned okio dependency in dependencyManagement that is no longer needed, as the okio dependency used by the more current okhttp is more recent, and has no known vulnerabilities. 

kotlin.version was also updated in hapi-fhir-base-test-jaxrsserver-kotlin as this was old and incompatible with the kotlin used in the new okio. This was been approved by @JPercival in a related PR:  

This also brings in a quality of life improvement from  which manages the spotbugs-annotations version via a property instead of literal versions. See comment thread in another PR here:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0cb7efbd860`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.