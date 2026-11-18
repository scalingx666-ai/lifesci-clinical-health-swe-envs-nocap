# Issue

**Title:** Free host disk space before nightly SNAPSHOT deploy job

## Description

The WAR assembly step for hapi-fhir-jpaserver-uhnfhirtest has been failing with "No space left on device" on the Microsoft-hosted agent. Remove the preinstalled .NET/Android/Haskell SDKs the image ships with before the build starts to reclaim that space.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e7129efb581`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.