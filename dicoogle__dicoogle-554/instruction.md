# Issue

**Title:** Fix plugin categorization in management page

## Description

Fixes a regression from #523, where plugins in the management page were not presented correctly in their respective categories.

![Capture-dicoogle-bug-before](https://user-images.githubusercontent.com/4738426/147589797-184b5d05-809a-4a56-9a66-e2b501a5bc04.PNG)

After the fix:

![Capture-dicoogle-bug-after](https://user-images.githubusercontent.com/4738426/147589792-25f9fec5-a1a8-495a-8c0b-b5681431f953.PNG)

- revert to filtering plugins by requested type
   - `getPlugins(type)` is planned but not yet available
- ensure that plugin categorization still works with mixed types of plugins anyway

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9a339131e342`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.