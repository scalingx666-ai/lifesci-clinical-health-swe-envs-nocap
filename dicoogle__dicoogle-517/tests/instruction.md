# Issue

**Title:** Fix server error on /webui without user session

## Description

500 would emerge if a webplugin is installed and a /webui request without an authenticated user would fetch it

This is a regression from #497, emerged once the PR was tweaked to let administrators see all web UI plugins. If the token does not refer to a valid session, `user` is null.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5507ee7d8b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.