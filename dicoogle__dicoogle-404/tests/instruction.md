# Issue

**Title:** Bug/webapp/plugins services

## Description

The DicoogleClient API was updated. Thus, the request in the WebApp got outdated. This PR fixes the issues in Management > Services and Plugins > Plugins.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47ab61432fb5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.