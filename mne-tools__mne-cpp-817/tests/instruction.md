# Issue

**Title:** [ENH] MNE Scan: writetofile changes

## Description

- Add some file utility functions to the utils library. (copy, rename, delete, create)
- Add element to MNE Scan WriteToFile to allow user to select different directories to save files to.
   - Prompt user to name file after recording.
   - Appends '.fif' if not specified.
   - Checks for existing file and prompt confirmation of overwrite or not.
   - Option to cancel save deletes file.

![save1](https://user-images.githubusercontent.com/34070103/134947876-f3c751de-8f53-457f-8d28-5601519a56c8.png)

![save2](https://user-images.githubusercontent.com/34070103/134947898-112bb14d-963e-4a1b-a08f-ef354a1aa5d2.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `423c240360dd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.