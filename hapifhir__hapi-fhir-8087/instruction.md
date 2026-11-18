# Issue

**Title:** Migrate hapi-fhir GitHub Actions CI builds to Java 21

## Description

Bump the JDK used by the GitHub Actions PR/test pipeline, release, and spotless workflows (and their composite actions) from 17 to 21. Source/ target compatibility stays at Java 17: maven.compiler.release=17 makes javac reject any post-17 API even when compiling on JDK 21. Also fix the deprecated 'adopt' distribution (no Java 21) to 'temurin' in generate-module-list, and clarify the maven-enforcer requireJavaVersion rule (now [17,)) and its message.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5e961542805b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.