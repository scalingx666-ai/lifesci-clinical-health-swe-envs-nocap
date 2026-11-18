# Issue

**Title:** Fixed the db query to get LocalChangeResourceReferenceEntity.

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

 

**Description**
Issue: 
As pointed by @LZRS in the #2495 description ,
The sql query  in the `LocalChangeDao.getReferencesForLocalChanges `should use `IN` operator instead of `=` operator to fetch all LocalChangeResourceReferenceEntity for the passed LocalChange ids.

Changes:
1. Updated sql query to use `IN`.
2. Added test to check the usage of `LocalChangeDao.getReferencesForLocalChanges ` with single and multiple LocalChange .

**Alternative(s) considered**
Have you considered any alternatives? And if so, why have you chosen the approach in this PR?

**Type**
Choose one: Bug fix

**Screenshots (if applicable)**

**Checklist**
- [x] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [x] I have read the [Contributing](https://github.com/google/android-fhir/wiki/Contributing) page.
- [x] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [x] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [x] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [x] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [x] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `693b8c6de2ba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.