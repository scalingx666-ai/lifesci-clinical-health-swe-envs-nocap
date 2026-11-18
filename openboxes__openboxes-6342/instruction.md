# Issue

**Title:** Remove duplicate import statements

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** none, small tech-debt cleanup.

**Description:**

Eight Groovy files import the same classes twice, usually because a block of imports was copied twice. This removes only the repeated lines (21 in total). The first import of each class stays, so behaviour is unchanged.

- grails-app/domain/org/pih/warehouse/core/Synonym.groovy
- grails-app/domain/org/pih/warehouse/picklist/Picklist.groovy
- grails-app/domain/org/pih/warehouse/product/ProductPackage.groovy
- grails-app/domain/org/pih/warehouse/receiving/ReceiptItem.groovy
- grails-app/services/org/pih/warehouse/data/DataService.groovy
- grails-app/taglib/org/pih/warehouse/AuthTagLib.groovy
- grails-app/taglib/org/pih/warehouse/InventoryTagLib.groovy
- test/unit/org/pih/warehouse/picklist/PicklistServiceTests.groovy

Found with groovyfmt, a Groovy linter, while testing it against this codebase.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c44432c3d0dd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.