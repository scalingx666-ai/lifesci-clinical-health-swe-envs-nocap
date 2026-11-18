# Issue

**Title:** Fix CI test failures due to US Core 5 artifacts

## Description

This PR fixes the failing CI tests, which I believe are because certain US Core 5 ValueSets don't contain relevant codes directly, they reference other valuesets. (Why the tests used to work and suddenly stopped one day a few weeks ago... I don't have an answer for that)

This does a few things:
 - Brings in the referenced value sets for "ONC Administrative Sex", "Race", "Ethnicity", "Unknown or refused to answer", and "Other or unknown or refused to answer". The HAPI validator is smart enough to be able to find these when trying to validate whether codes belong to, for example, the US Core birthsex valueset which references the ONC one.
 - Replaces the official US Core DocumentReference Type compose (which points to LOINC with type DOC) with the two specific LOINC codes we actually use. This was apparently what we did for R4 already: see 
 - Adds methods to ValidationResources so that we can either get a STU3 or R4 version. Since the objects here aren't static, there's no reason to load the STU3 artifacts for the R4 test, or vice versa.
 - Adds parameters to the ValidationSupportR4 to select whether US Core 4 or 5 (or both or neither) should be loaded. I can change this into an enum if people would prefer
 - Prevents toggling static fields back & forth between values in the FHIRR4ExporterTest as that seemed to be creating weird combinations in testing. Now there are 3 sub-tests with specific combinations of parameters.
 - Adds support to the ParallelTestingService to request fewer than 10 people. (so that the above test remains consistent on time, instead of running 3x as long. I think this is one of the longest tests already)

---
Also addresses the unrelated US Core 5 bug:
 - Changes the homelessness module observation category codes from "social-history" to "survey" to fix #1283 . Basically these observation get tagged as US Core profile "sdoh assessment" based on the code, and the "sdoh assessment" profile is a subprofile on "survey" so it requires a category of "survey". (Ideally I think these observations would have both categories, "social-history" AND "survey", but we don't support 2 categories in Synthea and I don't particularly want to hardcode adding a second category for just this code)
 - And finally fixes the reversed probabilities for Low SES homelessness since I was in the module anyway - #656

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f933a7111e5e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.