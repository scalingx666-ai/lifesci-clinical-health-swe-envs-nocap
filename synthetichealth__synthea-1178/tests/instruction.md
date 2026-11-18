# Issue

**Title:** FHIR export resource type filter

## Description

Addresses #1104

Adds new config settings to support filtering the resource types that are exported in the FHIR exporter, by either an include list or exclude list. (Similar to the existing feature for CSVs)
This approach checks each resource type before instantiating the relevant HAPI resource class.

A few notes on current status:
 - this leaves the Patient and Encounter resources as always included, even if specifically excluded, primarily because of the number of changes it would require.  
 - this doesn't currently attempt to be "friendly" and include related resources, for example a DiagnosticReport will reference Observations, but if you include DiagnosticReport without including Observation, you will get a DiagnosticReport with no outgoing references. 
 - this is only FHIR R4, but I'd like to get any feedback before applying this to the other exporters. (Or maybe we don't even want to spend time on the DSTU2 and STU3 exporters anymore?)
 - I'd also like to explore some changes to work with resource type enums instead of strings

This also includes a tweak to build.gradle to fix some error messages I was seeing in Eclipse. The issue was that JSBCL includes JUnit 4.10 as a transitive dependency, but we use JUnit 4.13 as a direct dependency for tests. Eclipse was getting confused and using JUnit 4.10 at compile time and it didn't recognize some method calls. The tweak removes the transitive dependency on JUnit from JSBCL because I don't think there's any need for the main build to include JUnit.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2fd1e9642436`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.