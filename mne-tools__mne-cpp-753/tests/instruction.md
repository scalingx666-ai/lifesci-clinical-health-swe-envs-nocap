# Issue

**Title:** [FIX] Make filter freq response graph respond to Default/Dark styles

## Description

text color in the FilterPlotScene class is now dependant on the FilterDesignView colors, which is, in turn, dependent on the Qt stylesheet applied to the class. Therefore, modifying the stylesheet, will now modify the text color used when ploting the frequency response.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d8cc22b2ae38`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.