# Issue

**Title:** Update columns' order in TokenIndexEntity multi-column index

## Description

**IMPORTANT: All PRs must be linked to an issue (except for extremely trivial and straightforward changes).**

**Description**
Updates the order of columns in the multi-column index used in the `TokenIndexEntity` entity table to have `index_value` as the leftmost column. 
Also removes  the `index_system` column from the index since it would never get used  because the queries generated use the IFNULL statement that forces evaluation from the actual rows.

With an example query

```sql
SELECT a.*
FROM ResourceEntity a
WHERE a.resourceType = 'Task'
  AND a.resourceUuid IN (SELECT resourceUuid
                         FROM TokenIndexEntity
                         WHERE resourceType = 'Task'
                           AND index_name = 'status'
                           AND (
                             (index_value = 'ready' AND IFNULL(index_system, '') = 'http://hl7.org/fhir/task-status') OR
                             (index_value = 'in-progress' AND
                              IFNULL(index_system, '') = 'http://hl7.org/fhir/task-status')));
```
**Previous** query plan, was
```
QUERY PLAN
|--SEARCH a USING INDEX index_ResourceEntity_resourceType_resourceId (resourceType=?)
`--LIST SUBQUERY 1
   `--SEARCH TokenIndexEntity USING COVERING INDEX index_TokenIndexEntity_resourceType_index_name_index_system_index_value_resourceUuid (resourceType=? AND index_name=?)
```
The **updated** query plan would be
```
QUERY PLAN
|--SEARCH a USING INDEX index_ResourceEntity_resourceType_resourceId (resourceType=?)
`--LIST SUBQUERY 1
   `--MULTI-INDEX OR
      |--INDEX 1
      |  `--SEARCH TokenIndexEntity USING INDEX index_TokenIndexEntity_index_value_resourceType_index_name_resourceUuid (index_value=? AND resourceType=? AND index_name=?)
      `--INDEX 2
         `--SEARCH TokenIndexEntity USING INDEX index_TokenIndexEntity_index_value_resourceType_index_name_resourceUuid (index_value=? AND resourceType=? AND index_name=?) 
```

**Type**
Feature

**Checklist**

- [ ] I have read and acknowledged the [Code of conduct](https://github.com/google/android-fhir/blob/master/CODE_OF_CONDUCT.md).
- [ ] I have read the [Contributing](https://google.github.io/android-fhir/contrib/) page.
- [ ] I have signed the Google [Individual CLA](https://cla.developers.google.com/about/google-individual), or I am covered by my company's [Corporate CLA](https://cla.developers.google.com/about/google-corporate ).
- [ ] I have discussed my proposed solution with code owners in the linked issue(s) and we have agreed upon the general approach.
- [ ] I have run `./gradlew spotlessApply` and `./gradlew spotlessCheck` to check my code follows the style guide of this project.
- [ ] I have run `./gradlew check` and `./gradlew connectedCheck` to test my changes locally.
- [ ] I have built and run the demo app(s) to verify my change fixes the issue and/or does not break the demo app(s).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `507e89cc8b75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.