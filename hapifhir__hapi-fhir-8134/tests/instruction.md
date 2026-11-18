# Issue

**Title:** Fix nightly SNAPSHOT central-publish job getting force-cancelled mid-…

## Description

…upload

Azure's default 60-minute job timeout was racing the central-publishing plugin's own 30-minute waitMaxTime, force-killing the job before the plugin could report a real timeout error. Set an explicit 90-minute job timeout (matching snapshot-release-pipeline.yml's convention) and make waitMaxTime/waitPollingInterval explicit in the central-repo profile instead of relying on plugin defaults.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3c84fb9ab18`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.