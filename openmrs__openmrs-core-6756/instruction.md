# Issue

**Title:** Scope the Get Roles proxy privilege to the implicit role read

## Description

## Description of what I changed

- Move the `Get Roles` proxy privilege out of the generic `@Authorized` check path and into `UserContext`'s implicit-role lookup, the only read that needs it
- Drop the duplicated privilege from the Spring Security path in `PrivilegeResolution`
- Add the `Get Roles` privilege and its `Authenticated` grant to `initialInMemoryTestDataSet.xml`, plus `RoleReadAuthorizationTest` for granted and denied role reads and a logged-out `@Authorized(Get Roles)` regression case in `OpenmrsAuthorizationManagerFactoryTest`

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the code style of this project.
- [x] I have added tests to cover my changes.
- [x] I ran `./mvnw clean package` right before creating this pull request and added all
  formatting changes to my commit.
- [x] All new and existing tests passed.
- [x] My pull request is based on the latest changes of the master branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a386f6a81db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.