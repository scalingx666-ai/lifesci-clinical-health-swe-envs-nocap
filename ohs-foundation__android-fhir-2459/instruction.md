# Issue

**Title:** Mechanical reformat of .github/workflows

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

Related to #2232

**Description**

This is a mechanical reformat of the x2 YAML in `.github/workflows`.

It was done by https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-github-actions.

This makes future changes easier to review.

**Type**
Choose one: Builds

**Checklist**
- [X] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [X] I have read the [Contributing](https://github.com/google/android-fhir/wiki/Contributing) page.
- [X] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [X] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [ ] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [ ] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [ ] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e06416c20f3b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.