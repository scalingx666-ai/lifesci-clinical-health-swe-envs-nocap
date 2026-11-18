# Issue

**Title:** Publish GitHub pages with explicit GitHub Action Steps

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

Related to #2232

**Description**

This PR contains x3 Commits. You may want to review and merge #2459 and then #2460 separately, first? Or all together here - your call.

I'm intentionally raising small changes; this alone doesn't "do" all that much, yet; my plan is to gradually build upon this.

This step should, if it works, make the exact same website content that we currently have up on https://google.github.io/android-fhir/ re-appear.

What changes is that instead of GitHub "implicitly" building it for us, via its https://github.com/google/android-fhir/actions/workflows/pages/, we "control" it - which allows us hook our own documentation build steps into it.

All the magic GitHub Workflow Action YAML gobbledygook introduced here is inspired by https://github.com/enola-dev/enola/blob/ed2b1755b9dbf1a0668c86f80048d8bded94de4a/.github/workflows/ci.yaml#L131, where I learnt how to do this to create https://docs.enola.dev.

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0467e57257ac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.