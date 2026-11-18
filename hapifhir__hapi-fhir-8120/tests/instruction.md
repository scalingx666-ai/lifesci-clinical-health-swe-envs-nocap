# Issue

**Title:** Allow search operations to use custom IBundleProvider as return type

## Description

Currently it is not possible to create a subclass of IBundleProvider and use that as the return type of a search operation. The return type has to be IBundleProvider. This could result in casting behavior in other places of the HAPI application.

In order to avoid casting, we can allow subclasses of IBundleProvider to be used as return type.

In our project, we have a IBundleProvider that holds additional information, like how the database is being queried. In places where we know the search operation beforehand, we would like to make use of the concrete return type instead of IBundleProvider without explicit casting.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1cca8e7d2556`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.