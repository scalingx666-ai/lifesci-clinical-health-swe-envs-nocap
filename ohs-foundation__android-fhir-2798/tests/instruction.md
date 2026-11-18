# Issue

**Title:** Use toSpanned in validation error dialog text

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**



**Description**
Use toSpanned in validation error dialog text

**Alternative(s) considered**
Another way is to remove the HTML, to only extract the text content.
But, just using toSpanned is much simpler.

**Type**
Bug fix

**Screenshots (if applicable)**
<img width="350" alt="Screen Shot 2025-02-21 at 15 31 57" src="https://github.com/user-attachments/assets/abfc32e4-dca2-4a87-b40a-3d71d0cfc81b" />


**Checklist**

- [x] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [x] I have read the [Contributing](https://google.github.io/android-fhir/contrib/) page.
- [x] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [x] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [x] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [x] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [x] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc692a8c258a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.