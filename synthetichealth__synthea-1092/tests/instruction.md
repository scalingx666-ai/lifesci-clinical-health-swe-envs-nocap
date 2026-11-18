# Issue

**Title:** Avoid NPE on looking up provider location references.

## Description

Avoid a rare NPE on FHIR export.

```
org.mitre.synthea.export.FHIRR4ExporterTest > testFHIRR4Export FAILED
    java.lang.NullPointerException
        at org.mitre.synthea.export.FhirR4.findLocationUrl(FhirR4.java:883)
        at org.mitre.synthea.export.FhirR4.encounter(FhirR4.java:773)
        at org.mitre.synthea.export.FhirR4.convertToFHIR(FhirR4.java:268)
        at org.mitre.synthea.export.FhirR4.convertToFHIRJson(FhirR4.java:355)
        at org.mitre.synthea.export.FHIRR4ExporterTest.lambda$testFHIRR4Export$0(FHIRR4ExporterTest.java:114)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6425dc723474`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.