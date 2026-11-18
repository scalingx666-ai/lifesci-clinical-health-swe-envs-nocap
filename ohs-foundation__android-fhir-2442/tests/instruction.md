# Issue

**Title:** Updated PerResourcePatchGenerator  to return ordered PatchMapping to avoid referential integrity issues.

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

Fixes #[issue number]


**Description**
1. Create a Directed Graph based on all the outgoing references for each Patch. Since the referential integrity comes to picture if the resource is not created yet, the edges of the graph are only the outgoing references to resources that are getting created during this upload. This may helps avoid some cycles as well.
2. The references are taken from `LocalChangeResourceReferenceEntity` which stores each outgoing references associated with a particular `LocalChange` as new entry.
3. Order the Patches so that if the resource A has outgoing references {B,C} (CREATE) and {D} (UPDATE), then B,C needs to go before the resource A so that referential integrity is retained. Order of D shouldn't matter for the purpose of referential integrity.

**Alternative(s) considered**
1. Splitting changes to CREATE first and subsequent UPDATE, but this would also require ordering the the create list incase it can overflow to multiple Bundles.  This would be similar to the current approach but, would require multiple PUSH for the same resource incase the resource was Created and then Updated on the device before being pushed to the server.

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee810d6a8cda`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.