# Issue

**Title:** [ENH] MNE Scan: change plugin gui items

## Description

- Sets the bounding rectangle around the text based on the size of the printed text with the used QPainter object.

#### For reference:


Plugin GUI now             |  Plugin GUI in this PR
:-------------------------:|:-------------------------:
![plugins_old](https://user-images.githubusercontent.com/34070103/150410077-63b9e5eb-f0f5-45e3-b9fa-5d11e7738a38.png)  |  ![plugins](https://user-images.githubusercontent.com/34070103/150409386-2d4c314c-b2a1-4297-84a7-4ca8c6756865.png)

Let me know if more/less spacing would look better. Or if we should look at doing line breaks on whitespace.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `811963f3d599`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.