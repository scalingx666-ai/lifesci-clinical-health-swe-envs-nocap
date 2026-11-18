# Issue

**Title:** Deduplicate hapi-tinder-plugin declaration in jpaserver-base

## Description

hapi-fhir-jpaserver-base declared ca.uhn.hapi.fhir:hapi-tinder-plugin twice in <build><plugins>: once for the generate-jparest-server executions and again for the generate-ddl executions. Maven keys plugins by groupId:artifactId, so the second declaration was a duplicate key and the model builder emitted:

```text
  [INFO] Scanning for projects...
  [WARNING] 
  [WARNING] Some problems were encountered while building the effective model for ca.uhn.hapi.fhir:hapi-fhir-jpaserver-base:jar:8.13.5-SNAPSHOT
  [WARNING] 'build.plugins.plugin.(groupId:artifactId)' must be unique but found duplicate declaration of plugin ca.uhn.hapi.fhir:hapi-tinder-plugin @ line 522, column 12
  [WARNING] 
  [WARNING] It is highly recommended to fix these problems because they threaten the stability of your build.
  [WARNING] 
  [WARNING] For this reason, future Maven versions might no longer support building such malformed projects.
  [WARNING] 
```

Fold the two into a single declaration: the generate-ddl executions join the existing <executions>, the hapi-fhir-jpaserver-model plugin dependency joins the existing <dependencies>, and the shared packageNames/dialects settings become the plugin-level <configuration>. This mirrors exactly what Maven was already producing when it merged the duplicate.

**Reviewer note** 
Verified: `mvn help:effective-pom -pl hapi-fhir-jpaserver-base` is byte-identical before and after, and `mvn clean process-classes` produces identical DDL for all 8 dialects in both the partitioned and nonpartitioned output directories.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5892fc1cd1fb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.