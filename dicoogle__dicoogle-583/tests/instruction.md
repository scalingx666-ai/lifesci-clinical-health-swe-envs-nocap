# Issue

**Title:** Encode text files and server text responses in UTF-8

## Description

, making it so that Unicode text values become properly visible in Dicoogle web app and web APIs.

- Override Jetty encoding properties so that responses are encoded in UTF-8.
- Also ensure that some files (tags.xml, roles.xml, CSV exports) are written in UTF-8.

![Screenshot dicoogle 2022-06-20 124645](https://user-images.githubusercontent.com/4738426/174611731-a4474203-9e12-49a9-9842-f6967360ee2e.png)

This might only break users expecting CSVs to be in the system's default encoding (or defined via JVM variables). As we are treating #522 as a bug, breaking such uses is an acceptable trade-off in favor of fully supporting Unicode and letting plugin implementers rely on UTF-8 for their web services.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a829486d3a18`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.