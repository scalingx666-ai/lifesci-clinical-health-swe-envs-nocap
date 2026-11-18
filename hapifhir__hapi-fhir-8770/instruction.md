# Issue

**Title:** Jm 2026028 add provided deps to repositories module

## Description

`hapi-fhir-repositories` pins required modules version but never declares them as provided dependencies, so they reach it only transitively, through `cqf-fhir-utility`. Maven builds its module graph from declared dependencies only, so there’s no edge from repositories to those modules. In sequential order the module happens to come after them, but with parallel builds it can start before they’re built, which fails if a new version is being built.

This PR declares the required modules as provided dependencies.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d07589c2cdc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.