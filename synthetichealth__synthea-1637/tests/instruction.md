# Issue

**Title:** Upgrade to Gradle 9 for JDK 25 support, remove JDK 11 support

## Description

This PR bumps the Gradle version to the latest as of today, 9.2.1, to enable support for JDK 25, the most recent LTS version of Java. Unfortunately this version of Gradle no longer supports JDK 11, so our new minimum will have to be JDK 17.

One group of dependencies needed to be updated to work with JDK 25 (GraalVM, which powers the JavaScript engine that runs Graphviz and one of the Flexporter actions) but other than that everything should work as is. Many thanks to those who upgraded the build.gradle file already to get it compatible with Gradle 9 for making this easy.

Addresses #1636 .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a934f8979d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.