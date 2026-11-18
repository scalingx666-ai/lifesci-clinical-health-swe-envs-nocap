# Issue

**Title:** Always use temporary directory when exporting to CSV

## Description

This is a recently discovered bug which could potentially affect everyone using the export to CSV functionality. The server's `Path` configuration was being used as the base folder for keeping temporary csv outputs (so that they can be subsequently downloaded), rather than a system's temporary folder. If the folder specified in `Path` did not exist, the operation would fail with an HTTP error code 500.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7dcfa5f01e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.