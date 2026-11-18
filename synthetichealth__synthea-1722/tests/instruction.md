# Issue

**Title:** fix: stop mutating Code in mapCodeToCodeableConcept

## Description

## Bug
`mapCodeToCodeableConcept` normalized its `Code` argument in place (`from.system = ExportHelper.getSystemURI(from.system)`). Module `Code` objects are process-wide singletons (shallow `State.clone()`), and `HealthRecord.Code.hashCode()` is built from `system`/`code` -- so the mutation leaked across patients AND across exporters. `Exporter` runs FHIR before CSV, so the CSV `SYSTEM` column read `SNOMED-CT` vs `http://snomed.info/sct` depending on the unrelated `exporter.fhir.export` flag: silent, order-dependent corruption of exported clinical data.

## Root cause
The in-place assignment existed in all three FHIR exporters:
- `src/main/java/org/mitre/synthea/export/FhirR4.java:3416`
- `src/main/java/org/mitre/synthea/export/FhirStu3.java:2465`
- `src/main/java/org/mitre/synthea/export/FhirDstu2.java:1798`

## Fix
Normalize into a local `String fromSystemURI` instead of writing back to `from.system`; the exported `Coding.system` is unchanged, only the caller's `Code` is left alone. Also documented the no-mutation contract in each method's javadoc.

Note on overlap: open PR #1708 applies this same change to `FhirR4.java` only (for #1702). The R4 hunk here is intentionally identical, so whichever PR merges second rebases trivially; this PR additionally covers `FhirStu3` and `FhirDstu2`, which #1708 does not.

## Test evidence
Added `testMapCodeToCodeableConceptDoesNotMutateCode` to `FHIRR4ExporterTest`, `FHIRSTU3ExporterTest`, and `FHIRDSTU2ExporterTest`. Each test builds a `Code("SNOMED-CT", "123456", "Test display")`, runs it through `mapCodeToCodeableConcept` (directly for R4, which is public; via reflection for the private STU3/DSTU2 variants), and asserts the source `Code.system` is still `SNOMED-CT` while the resulting coding carries `http://snomed.info/sct`.

Local verification (Gradle dependency resolution is unavailable in this sandbox, so `./gradlew test` could not run): compiled the three patched exporter files with `javac` against the released `synthea-with-dependencies.jar`, then ran standalone copies of the three new test methods via JUnit:
- against pristine classes: all 3 FAIL with `expected:<[SNOMED-CT]> but was:<[http://snomed.info/sct]>` (the mutation reproduces)
- against the patched classes: all 3 PASS, and the coding system URI is unchanged

The issue's end-to-end repro (`./gradlew uberJar`, two runs with/without `--exporter.fhir.export`, diff of the CSV `SYSTEM` column) was not run locally for the same reason. Requesting CI to confirm.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9d07a6eef91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.