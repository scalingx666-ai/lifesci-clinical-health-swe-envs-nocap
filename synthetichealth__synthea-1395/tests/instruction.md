# Issue

**Title:** Delete uncompressed sample data in deploy workflow

## Description

The deploy workflow with "autogenerate sample data" failed because the job runner ran out of disk space. This change deletes the uncompressed records (1k each of FHIR R4, STU3, DSTU2, CCDA, and CSV, so it's a lot) to save space.

Note, I made the change in the workflow instead of the generate_samples script because I don't want someone to run that script and accidentally delete data they want, and I put that step first so we could `rm ./output` without having to specify all the different subfolders and without affecting the javadoc folder.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56d48f71d4ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.