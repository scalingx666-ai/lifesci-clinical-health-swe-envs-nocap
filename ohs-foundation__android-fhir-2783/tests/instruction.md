# Issue

**Title:** Configure Review layout for SDC catalog application

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

 

**Description**
This change configures Review layout for SDC Catalog Application. It consist of the following updates:
1. Add new parameter `enableReviewMode` to Layout enum under `LayoutListViewModel.kt` and pass it as `true` for the REVIEW enum value along with `layout_review.json` to render questionnaire
2. Pass this parameter's value as an argument to `DemoQuestionnaireFragment.kt` and use it to show Review Page when its value is `true`
3. Fix `layout_review.json` to render questionnaire properly

**Alternative(s) considered**
N/A

**Type**
Bug fix

**Screenshots (if applicable)**
<img width="411" alt="Screenshot 2025-02-03 at 1 36 26 PM" src="https://github.com/user-attachments/assets/f7326c7c-6421-4e3e-81f1-63292b6462ce" />

**Checklist**

- [x] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [x] I have read the [Contributing](https://google.github.io/android-fhir/contrib/) page.
- [x] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [x] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [x] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [x] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [x] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d239e8e4e31`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.