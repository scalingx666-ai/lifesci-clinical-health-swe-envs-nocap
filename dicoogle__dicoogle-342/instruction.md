# Issue

**Title:** Use query providers that are DICOM

## Description

This targets the last update in #122. Two things that might be important to note:
- I used Java 8; since we are not supporting Java 7 anymore, I thought it would be ok;
- In `GET searchDIM/` I am ignoring providers that are not valid, instead of throwing an error; however, the web app is handling that, when using a multi-select that validates the providers; is it ok?

Also, possibly I forgot to apply the new settings somewhere. Please tell me if something is missing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `20bb385ff41a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.