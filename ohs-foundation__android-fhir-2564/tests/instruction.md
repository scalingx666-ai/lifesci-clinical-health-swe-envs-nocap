# Issue

**Title:** Pack repeated groups even if there is only one group in the response

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

**Description**
The current logic to pack repeated groups does not actually look at the questionnaire item at all. It simply packs multiple groups of the same id and assume they are from the same repeated group. This is fine unless if there is only one repeated group answer, the logic won't be able to distinguish this from non-repeated group.

The fix adds the questionnaire item to the logic so it packs if and only if it's a repeated group.

**Alternative(s) considered**
Have you considered any alternatives? And if so, why have you chosen the approach in this PR?

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a6f720cf382`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.