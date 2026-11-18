# Issue

**Title:** Update the purge API to accept a list of resource IDs

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

 

**Description**
1. Overloaded the `FhirEngine.purge` and modified `Database.purge` since has access modifier `internal` which is reused by the FhirEngine overloads.
2. In the implementation of `Database.purge`, wrapped the processing of the resource ids list in a transaction. Either they all pass or it fails.

**Alternative(s) considered**
Have you considered any alternatives? And if so, why have you chosen the approach in this PR?

**Type**
Feature

**Screenshots (if applicable)**
N/A

**Checklist**
- [x] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [x] I have read the [Contributing](https://github.com/google/android-fhir/wiki/Contributing) page.
- [x] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [x] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [x] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [x] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [x] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ff0643c68cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.