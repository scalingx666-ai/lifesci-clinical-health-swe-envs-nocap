# Issue

**Title:** fix(email): fetch URL attachments via safeFetch

## Description

Fetch http(s) attachment paths with safeFetch so outbound requests to private, link-local, and metadata addresses are blocked, including on redirect. Set disableUrlAccess so nodemailer never fetches URLs itself.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4e75ed351f7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.