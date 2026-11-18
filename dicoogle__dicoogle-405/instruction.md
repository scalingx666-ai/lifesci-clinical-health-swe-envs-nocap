# Issue

**Title:** Imp/configurable aetitle 282

## Description

This PR solves #282 

Implemented aetitle component in Management > Services & Plugins.

The AETitle is validated matching the ^[ A-Za-z0-9_.+-]*$ regex (only alphanumeric and _.+- characters are allowed) and a toast giving the status is shown whether the Save action is successful or not.

<img width="1680" alt="Screenshot 2019-12-19 at 12 17 08" src="https://user-images.githubusercontent.com/8323694/71172997-865e9280-2259-11ea-9e00-cdfe54faffdd.png">

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47ab61432fb5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.