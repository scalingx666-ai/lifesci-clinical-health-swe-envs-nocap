# Issue

**Title:** TRUNK-6328: Migrate to org.apache.groovy

## Description

<!--- Add a pull request title above in this format -->
<!--- real example: 'TRUNK-5111: Replace use of deprecated isVoided' -->
<!--- 'TRUNK-JiraIssueNumber: JiraIssueTitle' -->
## Description of what I changed
<!--- Describe your changes in detail -->
<!--- It can simply be your commit message, which you must have -->
Since `org.codehaus.groovy` was moved to `org.apache.groovy` when Groovy moved to the Apache
Software Foundation and the `org.codehaus.groovy` coordinates are no longer maintained.
This fix migrates openmrs-core to the latest Apache Groovy release.

Groovy 4+ no longer publishes the `groovy-all` fat jar, so `groovy-all` is now consumed as a
POM and every Groovy module ships at compile scope. `bom/pom.xml` therefore excludes the
tooling that server-side code doesn't need: the build modules (`groovy-ant`,
`groovy-docgenerator`, `groovy-groovydoc`), the desktop modules (`groovy-console`,
`groovy-swing`) and the interactive-shell modules (`groovy-groovysh`, `groovy-cli-picocli`),
plus `groovy-test` and `groovy-test-junit6`. The Groovy runtime modules (`groovy`,
`-datetime`, `-jmx`, `-json`, `-jsr223`, `-macro`, `-nio`, `-servlet`, `-sql`, `-templates`,
`-xml`, `-yaml`) stay, so modules using `JsonSlurper`, `XmlSlurper`, `groovy.sql.Sql` or
templates keep working. This keeps the WAR at 229 jars / 153.1 MB instead of 263 jars /
165.4 MB.

The explicit `jackson-dataformat-yaml` entry in the BOM pins the YAML module's Jackson
dependency to `${jacksonVersion}` (2.22.3), matching the rest of Jackson in the WAR;
`groovy-yaml` 6.0.0 declares 2.22.2 on its own.


## Issue I worked on
<!--- This project only accepts pull requests related to open issues -->
<!--- Want a new feature or change? Discuss it in an issue first! -->
<!--- Found a bug? Point us to the issue/or create one so we can reproduce it! -->
<!--- Just add the issue number at the end: -->
https://openmrs.atlassian.net/browse/TRUNK-6328

## Checklist: I completed these to help reviewers :)
<!--- Put an `x` in the box if you did the task -->
<!--- If you forgot a task please follow the instructions below -->
- [ ] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project.

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `891b80745b42`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.