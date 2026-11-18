# Issue

**Title:** TRUNK-6842: Voiding an encounter does not void its encounter provider…

## Description

…s (openmrs-core)

## Description of what I changed
https://openmrs.atlassian.net/browse/TRUNK-6842

## Issue I worked on
https://openmrs.atlassian.net/browse/TRUNK-6842

## Checklist: I completed these to help reviewers :)
<!--- Put an `x` in the box if you did the task -->
<!--- If you forgot a task please follow the instructions below -->
- [ X ] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project.

  No? Unsure? -> [configure your IDE](https://wiki.openmrs.org/display/docs/How-To+Setup+And+Use+Your+IDE), format the code and add the changes with `git add . && git commit --amend`

- [ X ] I have **added tests** to cover my changes. (If you refactored
  existing code that was well tested you do not have to add tests)

  No? -> write tests and add them to this commit `git add . && git commit --amend`

- [ X ] I ran `./mvnw clean package` right before creating this pull request and
  added all formatting changes to my commit.

  No? -> execute above command

- [ X ] All new and existing **tests passed**.

  No? -> figure out why and add the fix to your commit. It is your responsibility to make sure your code works.

- [ X ] My pull request is **based on the latest changes** of the master branch.

  No? Unsure? -> execute command `git pull --rebase upstream master`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `78481ccd081b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.