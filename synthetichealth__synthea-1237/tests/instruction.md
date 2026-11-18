# Issue

**Title:** Reproducibility fixes

## Description

Addresses #1236 and fixes some instances where running the same population multiple times produces different results

Issues identified and fixed so far:

1. The ordering of allergy reactions
2. DocumentReference content and Insurance plan selection

(Essentially both of these are the result of using Sets where order is not guaranteed. The current fix is not ideal, it does some extra sorting at the end, so there may be a more "root" fix further upstream. Note that I was not able to reproduce this second issue when running with only a single thread, which also suggests to me further analysis is required)

3. Resource UUIDs are occasionally different
This is because the UUIDs are generated using the same random number generator as used during generation. When the simulation is re-run with a different end date, the generation process may tick up an extra time stamp and roll a few extra random numbers. The fix here is to essentially remove all randomness from the FhirR4 exporter, done in two ways:
A) Select UUIDs during the generation process, by assigning them to every `HealthRecord.Entry` at creation time
B) For FHIR resources that don't align 1:1 with a synthea model class, use a new method `ExportHelper.buildUUID` to consistently create a UUID based on the Person, time, and a "key" for uniqueness. A few examples are the Provenance added to the end of each Bundle, DiagnosticRequests and DocumentReferences created for clinical notes, and ExplanationOfBenefits.

4. DICOM UIDs are occasionally different
This is because the Series object and the Instances it contains are being unintentionally leaked between patients. (Also doesn't occur when running with only a single thread.) I've put in a fix to ensure objects are always cloned, but I suspect there might be a more minimal fix possible. The "cleanest" would be an extra bit in `ImagingStudy.clone()` to match, for example, `ObservationGroup.clone()` where the observations in a list are individually cloned, but that's tougher in this case because we want certain instances to have a different/random number of objects in the list.

5. Differences across OSes
Observed on MacOS vs a Linux Docker image, likely to occur across other combinations as well. Patients with the same config were producing wildly different results. This was because in a couple places we were selecting a random index based on a HashMap, where sort order is not guaranteed. Seems like order is consistent for a given OS but still we shouldn't even bank on that. I replaced instances of HashMap with TreeMap for a minimal change that should ensure a consistent order.

Not currently implemented as part of this PR, I suggest we implement these separately:
 - FHIR 2 & 3 updates to match R4
 - CSV exporter to use the existing UUIDs
 - Update any other exporter that generates UUIDs
(Do we want these to be part of this PR?)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `340615e362a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.