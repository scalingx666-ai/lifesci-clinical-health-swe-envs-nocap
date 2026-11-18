# Issue

**Title:** Update calculated expression example to calculate age from date of birth

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

**Description**
Update calculated expression example to calculate age from date of birth.

See discussion https://chat.fhir.org/#narrow/stream/179266-fhirpath/topic/Calculating.20the.20period.20between.20two.20dates

The FHIRPath expression uses string manipulation to get the years of today's date and the date of birth, and calculate the age by substraction. It also compares the month and date parts of today's date and the date of birth to figure out if an additional year needs to be added to the result.

**Alternative(s) considered**
NA

**Type**
Bug fix

**Screenshots (if applicable)**

**Checklist**

- [x] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [x] I have read the [Contributing](https://google.github.io/android-fhir/contrib/) page.
- [x] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [x] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [x] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [x] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [x] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c224f7365726`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.