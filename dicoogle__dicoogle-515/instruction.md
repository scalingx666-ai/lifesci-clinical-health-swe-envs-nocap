# Issue

**Title:** Fix index settings `zip` property and remove it from UI

## Description

The "Index Zip Files" archive setting was not used anywhere in Dicoogle since version 2, which is why it was removed from the server settings in Dicoogle 3. However, it stayed as a visible property in the index settings service and in the user interface, which was misleadingly presented as enabled and could not even be changed in practice.

- Change index settings JSON output so that zip is `false` instead of the string `"false"`
   - We will treat this as a small regression of the Web API
- Remove the Index Zip Files row from the web UI
- Tweak "Indexation effort" to "Indexing effort", which is more accurate

The result:

![dicoogle-remove-zip-from-webapp](https://user-images.githubusercontent.com/4738426/135606671-5cdb7e69-33da-41e1-b793-c477c15dc681.PNG)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5507ee7d8b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.