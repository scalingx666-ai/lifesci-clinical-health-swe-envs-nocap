# Issue

**Title:** Fix typo to exclude junit:junit from org.ogce:xpp3 dependency

## Description

The junit dependency is wrongly a runtime dependency. it was tried to be excluded but there was a typo missing the exclude. Currently, this old unmaintained org.ogce:xpp3 is pulling junit:junit@4.7.0 which is not compatible with latest maven-surefire-plugin 3.6.0 which requires junit 4.11

it is causing this kind of error for project which has updated to maven-surefire-plugin 3.6.0 and depending on hapi-fhir:
```
Caused by: org.apache.maven.plugin.MojoExecutionException: Surefire is not compatible with JUnit 4.11 or older. Project version is 4.7
    at org.apache.maven.plugin.surefire.AbstractSurefireMojo$JUnitPlatformProviderInfo.getProviderClasspath (AbstractSurefireMojo.java:3224)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2abdabf8ef0f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.