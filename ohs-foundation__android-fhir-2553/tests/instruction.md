# Issue

**Title:** Improve search speed

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

 
As  in the above issue, this change reduces time from ~25 seconds to few milliseconds (7k patients).

**Description**
Remove extra JOIN clause (`a.resourceType = b.resourceType`). This clause is not needed as we already filter the resourceType in WHERE clause. 

Sample DSL search:-
```
fhirEngine.search<Patient> {
        sort(Patient.NAME, Order.ASCENDING)
        count = PaginationConstant.DEFAULT_PAGE_SIZE
        from = currentPage * PaginationConstant.DEFAULT_PAGE_SIZE
      }
```
Query before this change:-
```
SELECT a.resourceUuid, a.serializedResource
FROM ResourceEntity a
         LEFT JOIN StringIndexEntity b
                   ON a.resourceType = b.resourceType AND a.resourceUuid = b.resourceUuid AND b.index_name = 'name'
WHERE a.resourceType = 'Patient'
ORDER BY b.index_value ASC
LIMIT 20 OFFSET 0
```

Query after this change:-
```
SELECT a.resourceUuid, a.serializedResource
FROM ResourceEntity a
         LEFT JOIN StringIndexEntity b
                   ON a.resourceUuid = b.resourceUuid AND b.index_name = 'name'
WHERE a.resourceType = 'Patient'
ORDER BY b.index_value ASC
LIMIT 20 OFFSET 0
```
Notice that `a.resourceType = b.resourceType` clause is not present after `ON`.

**Alternative(s) considered**
None

**Type**
Choose one: (Bug fix | Feature | Documentation | Testing | Code health | Builds | Releases | Other)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b1c1b2750ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.