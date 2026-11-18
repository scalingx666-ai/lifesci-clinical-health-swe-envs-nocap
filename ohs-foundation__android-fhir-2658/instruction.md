# Issue

**Title:** Clean up UI navigation item

## Description

**Description**
This PR does three things:

1. Change the `QuestionnaireState`'s definition to include only one (or zero) `QuestionnaireAdapterItem.Navigation` instead of a list as it should never be the case that there are multiple navigation rows at the bottom
2. Remove the `isShown` and `isEnabled` in `QuestionnaireNavigationViewUIState` as these two properties were never used outside of tests. The semantics of the different UI states in the sealed class are not actuall meaningfully encoded in these two properties and the UI really just handles the different UI states like this: `if (state is HIDDEN) ... else if (state is ENABLED)` rather than `if (view.visibility = state.isShown) ... if(view.enabled = state.enabled)`.
3. Addressed warnings on using setters in the `QuestionnaireViewModelTests.kt`.

**Alternative(s) considered**
NA

**Type**
Code health

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f67501d4e0cd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.