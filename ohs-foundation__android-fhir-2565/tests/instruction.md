# Issue

**Title:** Balance SQLite expression tree for logical operators (AND/OR) to lower the depth

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

 

**Description**
Recursively bifurcates the conditional params expressions to prevent occurences of SQLite expression tree exceeding depth of 1000, as suggested in this 

**Alternative(s) considered**
Chunking large expression list to limit 50 within parantheses to avoid crashing with `Expression tree is too large (maximum depth 1000)`, as described [here](https://stackoverflow.com/a/17032196)

**Type**
Enhancement Feature

**Screenshots (if applicable)**

**Checklist**

- [ ] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [ ] I have read the [Contributing](https://google.github.io/android-fhir/contrib/) page.
- [ ] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [ ] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [ ] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [ ] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [ ] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `33206910294b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.