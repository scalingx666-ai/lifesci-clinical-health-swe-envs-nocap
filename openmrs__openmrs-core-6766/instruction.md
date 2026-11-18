# Issue

**Title:** INFRA: Add update rules for maintenance branches

## Description

<!--- Add a pull request title above in this format -->
<!--- real example: 'TRUNK-5111: Replace use of deprecated isVoided' -->
<!--- 'TRUNK-JiraIssueNumber: JiraIssueTitle' -->
## Description of what I changed
<!--- Describe your changes in detail -->
<!--- It can simply be your commit message, which you must have -->

We use dependabot to keep things up-to-date on master, but we have several other maintenance branches with different liveness rules. This adds support to 2.7 - 2.9 updating:

* GitHub Actions so we stay on supported versions of Node, etc.
* For 2.9.x, minor package versions
* For 2.7.x and 2.8.x any patch versions

The idea is that we allow dependencies to be kept up-to-date hopefully without breaking things.

A note about dependabot has been added to the README. Most things unchecked as this is a infrastructure-only change.

## Issue I worked on
<!--- This project only accepts pull requests related to open issues -->
<!--- Want a new feature or change? Discuss it in an issue first! -->
<!--- Found a bug? Point us to the issue/or create one so we can reproduce it! -->
<!--- Just add the issue number at the end: -->
see https://issues.openmrs.org/browse/TRUNK-

## Checklist: I completed these to help reviewers :)
<!--- Put an `x` in the box if you did the task -->
<!--- If you forgot a task please follow the instructions below -->
- [x] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project.

  No? Unsure? -> [configure your IDE](https://wiki.openmrs.org/display/docs/How-To+Setup+And+Use+Your+IDE), format the code and add the changes with `git add . && git commit --amend`

- [ ] I have **added tests** to cover my changes. (If you refactored
  existing code that was well tested you do not have to add tests)

  No? -> write tests and add them to this commit `git add . && git commit --amend`

- [ ] I ran `./mvnw clean package` right before creating this pull request and
  added all formatting changes to my commit.

  No? -> execute above command

- [ ] All new and existing **tests passed**.

  No? -> figure out why and add the fix to your commit. It is your responsibility to make sure your code works.

- [ ] My pull request is **based on the latest changes** of the master branch.

  No? Unsure? -> execute command `git pull --rebase upstream master`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0755f785f7d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.