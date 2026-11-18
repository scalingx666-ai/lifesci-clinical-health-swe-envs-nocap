# Issue

**Title:** Fix cursor moving back and missing characters

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

 

Cause of the issue: Sometimes processing of input is slower than the typing speed. This results into inconsistency between the answer stored in the QuestionnaireViewItem and the current text in the EditText. The UI is updated everytime the QuestionnaireViewItem is bound. So [here](https://github.com/google/android-fhir/blob/63151b5f1fdb6c1ad843d1421ea354b84fb51378/datacapture/src/main/java/com/google/android/fhir/datacapture/views/factories/EditTextStringViewHolderDelegate.kt#L68) we see the inconsistency where we use EditText#setText which does 2 things: Sets the EditText content to the answer in QuestionnaireViewItem (leading to missing character) AND also sets the cursor to beginning of the input.

Solution:-
1. Cursor does not go to the beginning: EditText#append moves the cursor to the last position.
2. Characters are not missed (skipped): We separate the validation update from input-text-box update. And we update the input text box only when the view is not in focus. This happens only when EITHER the RecyclerView loads a new question into the view OR there is a read-only question. This results into not updating the EditText programmatically for each user input.


~The EditText temporarily contains an extra character. The TextWatcher gets removed ([here](https://github.com/google/android-fhir/blob/63151b5f1fdb6c1ad843d1421ea354b84fb51378/datacapture/src/main/java/com/google/android/fhir/datacapture/views/factories/EditTextViewHolderFactory.kt#L104)) before it can process this extra character, leaving the saved text state (in QuestionnaireViewItem) inconsistent with the actual EditText content. This inconsistency triggers a UI update using EditText#setText ([here](https://github.com/google/android-fhir/blob/63151b5f1fdb6c1ad843d1421ea354b84fb51378/datacapture/src/main/java/com/google/android/fhir/datacapture/views/factories/EditTextStringViewHolderDelegate.kt#L68)), which unintentionally resets the cursor position to the beginning.~

~Read comments in rest of the PR for more details.~

**Description**
Clear and concise code change description. 

**Alternative(s) considered**
Have you considered any alternatives? And if so, why have you chosen the approach in this PR?

**Type**
Choose one: (Bug fix | Feature | Documentation | Testing | Code health | Builds | Releases | Other)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `541f69d85068`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.