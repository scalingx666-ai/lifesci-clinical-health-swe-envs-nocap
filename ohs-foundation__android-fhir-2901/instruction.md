# Issue

**Title:** Fix QuestionnaireItem's title styling in Header, for compose

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**
 

**Description**
This PR aims to fix `QuestionnaireItem` title header styling that I encountered while testing out the edit text compose work on OpenSRP's FHIRCore

**Alternative(s) considered**
Have you considered any alternatives? And if so, why have you chosen the approach in this PR?

**Type**
Choose one: (Bug fix | Feature | Documentation | Testing | Code health | Builds | Releases | Other)

**Screenshots (if applicable)**
### _Was_
<img width="50%" height="50%" alt="Screenshot_20251028_194521" src="https://github.com/user-attachments/assets/fc669314-1696-41c4-bd08-df6411fdf8f0" />

### _as opposed to_ 

<img width="50%" height="50%" alt="Screenshot_20251028_193945" src="https://github.com/user-attachments/assets/0c2c0b64-a2fd-4391-a843-bb94410cfc47" />

**Checklist**

- [ ] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [ ] I have read the [Contributing](https://google.github.io/android-fhir/contrib/) page.
- [ ] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [ ] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [ ] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [ ] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [ ] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5547a325c7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.