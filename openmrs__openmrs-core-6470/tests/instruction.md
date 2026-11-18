# Issue

**Title:** TRUNK-6777: Cache the tokenization of LayoutTemplates

## Description

<!--- Add a pull request title above in this format -->
<!--- real example: 'TRUNK-5111: Replace use of deprecated isVoided' -->
<!--- 'TRUNK-JiraIssueNumber: JiraIssueTitle' -->
## Description of what I changed
<!--- Describe your changes in detail -->
<!--- It can simply be your commit message, which you must have -->

We use LayoutTemplates to store how to format peoples names and addresses since our data model allows for a flexible set of fields with instance- determined meaning. These templates are called frequently, e.g., whenever we render a "full" or "short" name. In a single-threaded run, the run is dominated by the call to `getLines()` which on each invocation reparses the template. By cacheing this tokenization, we greatly speed up (~20x) the amount of time it takes to format a name. Since these templates are _very_ stable, this should be a net win on every operation that formats a user's name.

## Issue I worked on
<!--- This project only accepts pull requests related to open issues -->
<!--- Want a new feature or change? Discuss it in an issue first! -->
<!--- Found a bug? Point us to the issue/or create one so we can reproduce it! -->
<!--- Just add the issue number at the end: -->
see https://issues.openmrs.org/browse/TRUNK-6777

## Checklist: I completed these to help reviewers :)
<!--- Put an `x` in the box if you did the task -->
<!--- If you forgot a task please follow the instructions below -->
- [x] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project.

  No? Unsure? -> [configure your IDE](https://wiki.openmrs.org/display/docs/How-To+Setup+And+Use+Your+IDE), format the code and add the changes with `git add . && git commit --amend`

- [x] I have **added tests** to cover my changes. (If you refactored
  existing code that was well tested you do not have to add tests)

  No? -> write tests and add them to this commit `git add . && git commit --amend`

- [x] I ran `./mvnw clean package` right before creating this pull request and
  added all formatting changes to my commit.

  No? -> execute above command

- [x] All new and existing **tests passed**.

  No? -> figure out why and add the fix to your commit. It is your responsibility to make sure your code works.

- [x] My pull request is **based on the latest changes** of the master branch.

  No? Unsure? -> execute command `git pull --rebase upstream master`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c35fd0eb085`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.