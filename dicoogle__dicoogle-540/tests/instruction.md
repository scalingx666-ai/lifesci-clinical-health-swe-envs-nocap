# Issue

**Title:** Improve web UI manager asset fetching

## Description

This improves the manager of Web UI plugins for better performance, less chance of resource leaks, and reduced code size.

Summary:

- refactor parts of the class to use nio and apache commons APIs
- change internal routines to fetch text content eagerly
   - no more leaking zip entry
   - no more reading line by line, which is inefficient for reading large minified js files
- add test suite for loading a web UI plugin

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65eafc91ebc1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.