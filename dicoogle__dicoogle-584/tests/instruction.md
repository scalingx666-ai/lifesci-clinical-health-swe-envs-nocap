# Issue

**Title:** Add Instance Number to DIM search output and webapp image results

## Description

.

- In `images`, objects may also have a `number` field, which is present if the field is an integer.
- On the web app, a new column was added to the beginning of the search results table, on Image level.

![Screenshot from Dicoogle depicting part of the search results table, with column Instance # first](https://user-images.githubusercontent.com/4738426/174630163-8179eb79-db2c-4a06-a429-592b52d5888f.png)

This includes the necessary changes in GenericDIM plus extensions to documentation and a deprecation of an unused method which I believe is best removed in future versions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a829486d3a18`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.