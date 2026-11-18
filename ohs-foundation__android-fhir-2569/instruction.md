# Issue

**Title:** Check if previous/next page is hidden to show previous/next buttons

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

 

**Description**
Change `getQuestionnairePages` to only return questionnaire pages from QuestionnaireItems that have extension 
```
        {
          "url": "http://hl7.org/fhir/StructureDefinition/questionnaire-itemControl",
          "valueCodeableConcept": {
            "coding": [
              {
                "system": "http://hl7.org/fhir/questionnaire-item-control",
                "code": "page",
                "display": "Page"
              }
            ]
          }
        }
```

**Alternative(s) considered**
Have you considered any alternatives? And if so, why have you chosen the approach in this PR?

**Type**
Bug fix

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `736578fb4e2d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.