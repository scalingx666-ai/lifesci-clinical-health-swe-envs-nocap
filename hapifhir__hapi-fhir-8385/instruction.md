# Issue

**Title:** Skip the npm publish when the version is already published from this commit

## Description

When publishing a HAPI release, the npm publish would happen before the sonatype publish. 

If the sonatype publish fails, and you need to retry, the release pipeline will fail earlier since npm will try republishing the typescript artifacts, but the npm registry forbids republishing artifacts with an existing version number. 

The new script fixes this:
- If the version and commit SHA is the same as a published version, the npm publish is skipped automatically. 
- If the version is the same as a published version, but the commit SHA is different, reject with a message.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e4aa0103171`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.