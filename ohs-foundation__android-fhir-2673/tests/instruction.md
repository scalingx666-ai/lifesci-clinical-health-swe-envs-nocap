# Issue

**Title:** Add argument to disable Submit anyway button in the questionnaire confirmation popup

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

 

**Description**
Add bundle argument `EXTRA_SHOW_SUBMIT_ANYWAY_BUTTON` in `QuestionnaireFragment.kt` and `QuestionnaireValidationErrorMessageDialogFragment.kt` to optionally disable submit anyway if it's not needed. Default value for the same is `true`. 

Defines a setter in `QuestionnaireFragment.kt` so that it's value can be easily set while creating an instance of QuestionnaireFragment. Add Relevant test methods for the same

**Alternative(s) considered**
N/A

**Type**
Bug fix

**Screenshots (if applicable)**
N/A

**Checklist**

- [x] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [x] I have read the [Contributing](https://google.github.io/android-fhir/contrib/) page.
- [x] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [x] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [x] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [x] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [x] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7fd7d56ee7ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.