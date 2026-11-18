# Issue

**Title:** Allow a HAPI PR to point the CDR build at a specific CDR branch

## Description

Adds a !cdr-branch=<branch> marker, read from the pull request description and its comments, mirroring the !hapi-branch= marker on the CDR side. It takes effect after the workflow_dispatch input and before the rel_* branch map, so existing behaviour is unchanged when no marker is present.

**Reviewer Notes**

1. Compile against CDR step picked indicated branch. See `Compile against CDR` step fragment:

```text
Getting source from Git repository
Gitaly correlation ID: a39101adeb472a4a-CDG
Fetching changes with git depth set to 10...
Reinitialized existing Git repository in /builds/simpatico.ai/cdr/.git/
Created fresh repository.
Checking out 39382318 as detached HEAD (ref is 9155-smile-12697-mdm-support-multiple-eids-for-a-single-resource-type)...
Skipping Git submodules setup
```

2. Build failed as expected because indicated CDR branch has code incompatible with hapi branch, for validations purposes. Will remove pointer and perform successful build after approval.
(removed now to make build run against master to pass)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5892fc1cd1fb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.