# Issue

**Title:** Fix blob download for empty blobs

## Description

Bug: With some recent package updates, empty blobs are being returned as null instead of empty causing the download to fail.
Fix: Read as byte array and then get encoded string. This handles empty byte array and returns empty string.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7bdbaf92249`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.