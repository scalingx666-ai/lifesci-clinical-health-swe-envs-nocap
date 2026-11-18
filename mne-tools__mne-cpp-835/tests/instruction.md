# Issue

**Title:** [ENH] HPI Fit 3D View - multi view display

## Description

- Add 3 new cameras and viewports to 3dview (toggleable).
- Add controls to control3dview to select between single and multiview
- Make Multiview stack horizontally/vertically based on a available space and aspect ratio.

Here's what it looks like (disregard fit, it's sample_audvis_raw) 

![multiview1](https://user-images.githubusercontent.com/34070103/133802389-aea04e75-0be6-4ae0-8e87-4c74f85da122.png)

![multiview2](https://user-images.githubusercontent.com/34070103/133802398-fb861b06-d21e-479e-99ae-3ba3bbebb484.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6dfbef0e641e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.