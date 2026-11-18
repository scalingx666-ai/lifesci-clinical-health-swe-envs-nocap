# Issue

**Title:** OBPIH-8086 Move CI workflows and Docker image to Java 17 for Grails 7

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** OBPIH-8086

**Description:**
Grails 7.2.4 requires Java 17, and `build.gradle` already sets `sourceCompatibility`/`targetCompatibility` to 17.

**Status update:** `backend-tests.yml` on `feature/grails-7.2.4-upgrade` already uses Java 17, because that change came in with #6320 (via #6322). The diff against the new base is now just:

- `java-version: 17` in `dbdocs.yml`, `do-github-release.yml` and `docker-image.yml` (still `8` on the base)
- `docker/Dockerfile`: `eclipse-temurin:8-jre-jammy` → `eclipse-temurin:17-jre-jammy`. Without this, the release image would build the WAR with Java 17 and run it on a Java 8 runtime.

**What CI on this PR covers:** PR CI never runs any of the remaining changed files. These workflows only run on pushes to `develop`, on `v*` tags, or through `workflow_dispatch`, and dispatching them would publish a draft release, push a Docker image or update dbdocs. Things to check before the first release from this branch:
- `dbdocs.yml` and `do-github-release.yml` still call `./grailsw` (`schema-export` and `war`). I haven't checked that these commands still work under Grails 7.
- To check the Docker image locally: `./gradlew prepareDocker -Dgrails.env=prod`, then `docker build build/docker/`

---

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BqLUYCuzRWriJmqVjYmX8e

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `42ce71c5ee95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.