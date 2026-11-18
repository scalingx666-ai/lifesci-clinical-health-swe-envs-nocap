# Issue

**Title:** Fix issues in RolesXML

## Description

Addressing #361, this PR does some refactoring of the `RolesXML` class, also fixing a bug in the process where the `Roles` XML element was not being closed.

We might no longer have an issue with broken roles.xml files with this, but it would be nice to give all our configuration files the same treatment as the server settings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8748eac7e071`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.