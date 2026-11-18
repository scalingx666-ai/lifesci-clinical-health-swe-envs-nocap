# Issue

**Title:** Reading the keystore.type from mirth.properties

## Description

The mirth.properties file has a field keystore.type that is used to
specify the type of the keystore file. Currently it is unused, and
instead the type JCEKS is hardcoded in a few places.

This commit makes it so that the file type is correctly read from
the properties file.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e66d1122dbee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.