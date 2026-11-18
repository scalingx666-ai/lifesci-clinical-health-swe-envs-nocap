# Issue

**Title:** TRUNK-6764: Remove unused xercesImpl dependency

## Description

## Description of what I changed

Removed the unused `xerces:xercesImpl` dependency from OpenMRS Core.

* Removed `xerces:xercesImpl` from `api/pom.xml`.
* Removed the unused `xercesVersion` property from `bom/pom.xml`.
* Removed the `xercesImpl` dependency entry from the BOM.
* Removed the `xerces:xercesImpl` entry from `NOTICE.md`.

During review, @dkayiwa recommended adding a safeguard to prevent `xerces:xercesImpl` from being reintroduced transitively in the future. Although this was not explicitly requested in the issue, I implemented the recommendation by adding a Maven Enforcer `bannedDependencies` rule to the existing Enforcer configuration.

Before removing the dependency, I verified that no Java source imports `org.apache.xerces` and that the relevant XML parsing paths use JAXP APIs.

I also inspected the module configuration, Liquibase changelog, and HL7-related XML parsing paths to verify that they do not directly depend on the Xerces implementation.

The existing tests were left unchanged.

The `org.apache.xerces` entry in `checkstyle.xml` was left unchanged because it is an `IllegalImport` rule preventing Xerces imports, not a dependency declaration.

## Issue I worked on

See https://issues.openmrs.org/browse/TRUNK-6764

## Verification

* `mvn dependency:tree -Dincludes=xerces:xercesImpl` — **BUILD SUCCESS**; `xercesImpl` no longer appears in any module dependency tree.
* `ModuleFileParserUnitTest` — **BUILD SUCCESS**.
* `DatabaseUpdaterDatabaseIT` — **BUILD SUCCESS**.
* `./mvnw clean package` — **BUILD SUCCESS**.
* `mvn clean verify -DskipTests` — **BUILD SUCCESS**.
* `git diff --check` — clean.

## Checklist: I completed these to help reviewers :)

* [x] My IDE is configured to follow the [**[code style](https://wiki.openmrs.org/display/docs/Java+Conventions)**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project.

* [ ] I have **added tests** to cover my changes. (If you refactored
  existing code that was well tested you do not have to add tests)

* [x] I ran `./mvnw clean package` and added all formatting changes to my commit.

* [x] All new and existing **tests passed**.

* [x] My pull request is **based on the latest changes** of the master branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `000d3d8a071f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.