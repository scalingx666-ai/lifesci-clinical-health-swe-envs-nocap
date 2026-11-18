# Issue

**Title:** Dependency bumps

## Description

This PR bumps dependencies to eliminate some transitive dependencies on libraries with known vulnerabilities. It also eliminates the dependency on the Spring Framework (!) which was being used solely for its HTTP client. That has now been replaced by OkHttp, which was already a transitive dependency.

An update to the library that is used for URL validation started flagging URLs being constructed for value set expansions. This was fixed by URI encoding some of the characters in the URL, but this should be checked more closely.

This PR bumps the minimum version of Java required to run Synthea to Java 11. This is required to use hapi 6.x.

There are still known issues that will require deeper code changes to fix:
* Physiology - `cql-engine` and `cql-to-elm` both have vulnerabilities, but the underlying use of CQL will need to be changed to deal with changes in the environment. Perhaps more difficult is that this functionality relies on `jsmbl`, which has a critical vulnerability in its most recently released version.
* graphviz - `graphviz-java` needs to be updates, but API changes break existing code

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32478f4fd48a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.