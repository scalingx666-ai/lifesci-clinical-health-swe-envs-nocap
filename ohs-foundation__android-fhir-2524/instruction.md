# Issue

**Title:** Ordering of patches with cycles during upload

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**



**Description**

~~1. Find subgraphs (weakly connected) of Resources with cycles in them .
2. Pack the subgraphs in  Bundles such that a single subgraph is not split between two Bundles (as it may cause server error).
3. Order the remaining resources and add them to the Bundle (in remaining space of or new Bundles) .~~

1. Find the ordered strongly connected components of the Resource Graph.
2. Pack the sccs in Bundles such that a single scc is not split between two Bundles.

**Alternative(s) considered**
Have you considered any alternatives? And if so, why have you chosen the approach in this PR?

**Type**
Choose one: Bug fix

**Screenshots (if applicable)**

**Checklist**
- [ ] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [ ] I have read the [Contributing](https://github.com/google/android-fhir/wiki/Contributing) page.
- [ ] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [ ] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [ ] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [ ] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [ ] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10165589c4e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.