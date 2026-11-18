# Issue

**Title:** bug: include name and dob in DiffUtil content comparison

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**



**Description**
Fix patient list not refreshing after editing patient details by updating the PatientItemDiffCallback.areContentsTheSame() method to include name and dob field comparisons.
**Alternative(s) considered**
Option 1: Compare entire object (oldItem == newItem)

Pros: Catches all field changes automatically

Cons: May trigger unnecessary updates for internal fields not visible to users

I've found this solution being dismiss on this 

Option 2: Adapter workaround (submitList(null) then submitList(data))
<details> <summary>Code</summary>
<img width="648" height="124" alt="Screenshot 2025-09-18 at 6 57 08 PM" src="https://github.com/user-attachments/assets/8e2e584d-d2df-4887-bb1e-c6ad4ee92719" />
</details>

Pros: Quick fix that bypasses DiffUtil entirely
Cons: Loses DiffUtil's efficient animations and selective updates; treats symptom rather than cause

Option 3: Compare user-visible fields (chosen solution)

Pros: Fixes root cause while maintaining DiffUtil efficiency; updates only when UI-relevant data changes
Cons: Requires maintenance when display fields change

**Type**
Choose one: Bug fix

**Screenshots (if applicable)**
<details> <summary>Testing</summary>

https://github.com/user-attachments/assets/0758f45c-fca6-4500-a968-9aea46a4b9a3

</details>
**Checklist**

- [x] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [ ] I have read the [Contributing](https://google.github.io/android-fhir/contrib/) page.
- [x] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [x] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [x] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [x] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [x] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69d3e5c03a9a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.