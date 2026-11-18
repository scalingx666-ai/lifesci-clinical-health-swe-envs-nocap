# Issue

**Title:** [FIX] Update design filter freq response view

## Description

Two problems. When filterdesignview is created the filter freq response graph is also created and hidden. 
When a users clicks the button, the window is unhidden and, at least in windows, you see this:
 - 
![Screenshot 2021-01-15 165728](https://user-images.githubusercontent.com/8955424/104795570-6d3a5500-577d-11eb-8054-3ce2c78b0f25.png)


So we: 
 - make updateFilterPlot part of the public api. 
 - disable the scroll bar vert and horiz, because they kind of looked bad.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d418e36e5c3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.